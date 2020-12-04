<template>
  <h1>Hi</h1>
  <div>{{ msg }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import WalletConnectProvider from "@walletconnect/web3-provider";
import Web3Modal from "web3modal";
import {ethers} from "ethers";
let zksync;

async function connect() {
  zksync = await import('zksync');

  const providerOptions = {
    walletconnect: {
      package: WalletConnectProvider,
      options: {
        infuraId: "b818c25e42c049faa539560425a18a4e"
      }
    }
  };

  const web3Modal = new Web3Modal({
    network: "mainnet", // optional
    cacheProvider: false, // optional
    providerOptions // required
  });
  web3Modal.clearCachedProvider();

  const provider = await web3Modal.connect();

  const ethersProvider = new ethers.providers.Web3Provider(provider);
  const ethSigner = await ethersProvider.getSigner();
  console.log("sign: ", await ethSigner.signMessage("hello-world"));
  const zksyncProvider = await zksync.getDefaultProvider("mainnet", "HTTP");
  const wallet = await zksync.Wallet.fromEthSignerNoKeys(ethSigner, zksyncProvider);
  wallet.ethSignerType = {
   verificationMethod: "ERC-1271",
   // Indicates if signer adds `\x19Ethereum Signed Message\n${msg.length}` prefix before signing message.
   // i.e. if false, we should add this prefix manually before asking to sign message
   isSignedMsgPrefixed: true,
  }
  wallet.signer = zksync.Signer.fromSeed(new Uint8Array([1,2,3,4,5,6,7,8,9,1,2,3,4,5,6,7,8,9,1,2,3,4,5,6,7,8,9,1,2,3,4,5,6,7,8,9,1,2,3,4,5,6,7,8,9]))
  console.log(await wallet.isSigningKeySet())
  const tx = await wallet.onchainAuthSigningKey();
  console.log("tx: ", tx.hash);
  await tx.wait();

  const zktx = await wallet.setSigningKey({feeToken: "ETH", onchainAuth: true});
  console.log("zktx:", zktx.txHash);
}

connect();


export default defineComponent({
  name: 'App',
  props: {
    msg: String
  }
});

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
