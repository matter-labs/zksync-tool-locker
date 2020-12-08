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

export async function signMessagePersonalAPI(signer: ethers.Signer, message: Uint8Array): Promise<string> {
  if (signer instanceof ethers.providers.JsonRpcSigner) {
    return signer.provider.send('personal_sign', [ethers.utils.hexlify(message), await signer.getAddress()]).then(
        (sign) => sign,
        (err) => {
          // We check for method name in the error string because error messages about invalid method name
          // often contain method name.
          if (err.message.includes('personal_sign')) {
            // If no "personal_sign", use "eth_sign"
            return signer.signMessage(message);
          }
          throw err;
        }
    );
  } else {
    return signer.signMessage(message);
  }
}
async function connect() {
  zksync = await import('zksync');

  const providerOptions = {
    walletconnect: {
      package: WalletConnectProvider,
      options: {
        infuraId: "b818c25e42c049faa539560425a18a4e",
        // qrcode: false,
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
  const msg = ethers.utils.toUtf8String("0x5472616e7366657220302e3031204441490a546f3a203078346637353235363930633265333538303532356537396636636263623762386533366636366131310a4e6f6e63653a2032310a4665653a20302e30343736204441490a4163636f756e742049643a20323831353038");
  console.log("")
  console.log("sign: ", await ethSigner.signMessage(msg));
  console.log("sign personal: ", await signMessagePersonalAPI(ethSigner, ethers.utils.toUtf8Bytes(msg)));
  // const zksyncProvider = await zksync.getDefaultProvider("mainnet", "HTTP");
  // const wallet = await zksync.Wallet.fromEthSignerNoKeys(ethSigner, zksyncProvider);
  // wallet.ethSignerType = {
  //  verificationMethod: "ERC-1271",
  //  // Indicates if signer adds `\x19Ethereum Signed Message\n${msg.length}` prefix before signing message.
  //  // i.e. if false, we should add this prefix manually before asking to sign message
  //  isSignedMsgPrefixed: true,
  // }
  // wallet.signer = zksync.Signer.fromSeed(new Uint8Array([1,2,3,4,5,6,7,8,9,1,2,3,4,5,6,7,8,9,1,2,3,4,5,6,7,8,9,1,2,3,4,5,6,7,8,9,1,2,3,4,5,6,7,8,9]))
  // console.log(await wallet.isSigningKeySet())
  // const tx = await wallet.onchainAuthSigningKey();
  // console.log("tx: ", tx.hash);
  // await tx.wait();
  //
  // const zktx = await wallet.setSigningKey({feeToken: "ETH", onchainAuth: true});
  // console.log("zktx:", zktx.txHash);
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
