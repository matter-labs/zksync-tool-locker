<template>
  <h1>Method to disable CPK on ropsten</h1>
  <button type="button" id="modal-trigger">Open modal</button>
  <div>{{msg}}</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import WalletConnectProvider from "@walletconnect/web3-provider";
import Web3Modal from "web3modal";
import { ethers } from "ethers";
import { getDefaultProvider, Wallet as zkWallet, Signer as zkSigner } from "zksync";

export default defineComponent({
  name: "App",
  props: {
    msg: String
  }
})

const connect = async () => {

  const providerOptions = {
    walletconnect: {
      package: WalletConnectProvider,
      options: {
        infuraId: "72b13ae588b44eb9bc04c571bf22c984"
      }
    }
  };

  const web3Modal = new Web3Modal({
    network: "ropsten", // optional
    cacheProvider: false, // optional
    providerOptions // required
  });

  try {

    web3Modal.clearCachedProvider();

    const provider = await web3Modal.connect();

    console.log(provider);


    const ethersProvider = new ethers.providers.Web3Provider(provider);
    const ethSigner = await ethersProvider.getSigner();
    const signMessage = await ethSigner.signMessage("hello-world");
    console.warn("sign: ", signMessage);
    const zksyncProvider = await getDefaultProvider("ropsten", "HTTP");
    const wallet = await zkWallet.fromEthSignerNoKeys(ethSigner, zksyncProvider);
    wallet.ethSignerType = {
      verificationMethod: "ERC-1271",
      // Indicates if signer adds `\x19Ethereum Signed Message\n${msg.length}` prefix before signing message.
      // i.e. if false, we should add this prefix manually before asking to sign message
      isSignedMsgPrefixed: true
    };
    wallet.signer = await zkSigner.fromSeed(new Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3,
      4, 5, 6, 7, 8, 9]));
    const keySet = await wallet.isSigningKeySet();
    console.warn("is key set?:", keySet);
    const tx = await wallet.onchainAuthSigningKey();
    console.warn("tx: ", tx.hash);
    await tx.wait();

    const zkTx = await wallet.setSigningKey({ feeToken: "ETH", ethAuthType: "Onchain" });
    console.warn("zk txn link", `https://rinkeby.zkscan.io/explorer/transactions/${zkTx.txHash}`);
  } catch (error) {
    console.error(error);
    alert(error.message);
  }
};

document.addEventListener('readystatechange', () => {
  document.querySelector('#modal-trigger')?.addEventListener('click', connect)
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
