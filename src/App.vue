<template>
  <div class="sm:hidden absolute top-4 left-0 w-full px-4">
    <label for="tabs" class="inline-flex mb-2 text-sm text-gray-300">Choose network</label>
    <hr>
    <select name="tabs" class="block w-full focus:ring-indigo-500 focus:border-indigo-500 border-gray-300 rounded-md" v-model="currentNetwork">
      <option v-for="(network) in ['ropsten', 'rinkeby', 'mainnet']" :key="`mobile-${network}`">{{ network }}</option>
    </select>
  </div>
  <div class="flex-shrink-0 flex justify-center">
    <a href="/" class="inline-flex">
      <span class="sr-only">zkSync {{ currentNetwork }}</span>
      <a href="https://zksync.io" target="_blank">
        <svg fill="none" class="h-8 w-auto" viewBox="0 0 1407 276" xmlns="http://www.w3.org/2000/svg">
          <path clip-rule="evenodd" d="M485.481 137.772L347.819.254944V100.967L211.134 201.801L347.819 201.896V275.289L485.481 137.772Z" fill="#4E529A"
                fill-rule="evenodd"></path>
          <path clip-rule="evenodd" d="M0.200116 137.722L137.862 275.239L137.862 175.337L274.547 73.6923L137.862 73.5981L137.862.205097L0.200116 137.722Z" fill="#8C8DFC"
                fill-rule="evenodd"></path>
          <path d="M697.395 218.752H591.773V188.421L652.239 121.018H593.33V91.2059H696.357V119.982L634.073 188.68H697.395V218.752Z" fill-opacity="0.9" class="logoLetter"></path>
          <path d="M841.54 91.2059L790.416 144.869L842.578 218.752H800.278L766.541 170.015L752.268 185.051V218.752H717.752V31.0623H752.268V138.647L796.385 91.2059H841.54Z"
                fill-opacity="0.9" class="logoLetter"></path>
          <path
            d="M991.66 78.7624L959.48 88.6135C958.269 82.0461 954.982 76.0836 949.619 70.726C944.256 65.3684 936.384 62.6895 926.003 62.6895C917.526 62.6895 910.605 65.0227 905.242 69.689C899.879 74.1825 897.197 79.6265 897.197 86.0211C897.197 97.2548 903.858 104.168 917.18 106.76L942.871 111.686C959.134 114.797 971.764 121.278 980.76 131.129C989.757 140.98 994.255 152.559 994.255 165.867C994.255 181.076 988.2 194.383 976.089 205.79C964.152 217.024 948.062 222.64 927.82 222.64C916.228 222.64 905.761 220.912 896.418 217.456C887.076 213.999 879.55 209.419 873.841 203.716C868.132 197.84 863.633 191.704 860.346 185.31C857.232 178.742 855.329 172.002 854.637 165.089L887.855 156.275C888.72 166.126 892.526 174.335 899.273 180.903C906.194 187.47 915.796 190.754 928.079 190.754C937.422 190.754 944.688 188.68 949.878 184.532C955.242 180.384 957.923 174.94 957.923 168.2C957.923 162.842 955.934 158.263 951.954 154.46C948.148 150.485 942.698 147.807 935.605 146.424L909.913 141.239C895.034 138.128 883.27 131.993 874.619 122.833C865.969 113.673 861.644 102.267 861.644 88.6135C861.644 72.3678 867.872 58.7146 880.329 47.6537C892.958 36.5928 908.097 31.0623 925.744 31.0623C936.297 31.0623 945.726 32.5313 954.031 35.4694C962.335 38.4074 968.996 42.3824 974.013 47.3944C979.03 52.2336 982.923 57.2455 985.691 62.4303C988.459 67.6151 990.449 73.0591 991.66 78.7624Z"
            fill-opacity="0.9" class="logoLetter"></path>
          <path d="M1052.4 269.044H1015.81L1045.91 202.679L991.674 91.2059H1030.34L1064.34 165.867L1095.74 91.2059H1132.59L1052.4 269.044Z" fill-opacity="0.9"
                class="logoLetter"></path>
          <path
            d="M1180.23 145.387V218.752H1145.71V91.2059H1179.19V107.02C1182.82 100.798 1188.01 96.0451 1194.76 92.7613C1201.51 89.4776 1208.6 87.8358 1216.04 87.8358C1231.09 87.8358 1242.51 92.5885 1250.3 102.094C1258.26 111.427 1262.24 123.524 1262.24 138.388V218.752H1227.72V144.35C1227.72 136.746 1225.73 130.61 1221.75 125.944C1217.94 121.278 1212.06 118.945 1204.1 118.945C1196.84 118.945 1191.04 121.451 1186.72 126.463C1182.39 131.474 1180.23 137.783 1180.23 145.387Z"
            fill-opacity="0.9" class="logoLetter"></path>
          <path
            d="M1346.83 119.204C1337.66 119.204 1329.96 122.401 1323.74 128.796C1317.51 135.19 1314.39 143.918 1314.39 154.979C1314.39 166.04 1317.51 174.854 1323.74 181.421C1330.14 187.816 1337.92 191.013 1347.09 191.013C1355.22 191.013 1361.71 188.939 1366.56 184.791C1371.4 180.471 1374.69 175.372 1376.42 169.496L1406.78 179.607C1403.67 191.359 1396.92 201.469 1386.54 209.938C1376.16 218.406 1363.01 222.64 1347.09 222.64C1328.06 222.64 1312.06 216.246 1299.08 203.457C1286.28 190.495 1279.88 174.335 1279.88 154.979C1279.88 135.449 1286.19 119.29 1298.82 106.501C1311.63 93.7119 1327.37 87.3173 1346.05 87.3173C1362.32 87.3173 1375.64 91.5516 1386.02 100.02C1396.4 108.316 1403.06 118.426 1406 130.351L1375.12 140.721C1370.97 126.376 1361.54 119.204 1346.83 119.204Z"
            fill-opacity="0.9" class="logoLetter"></path>
        </svg>
      </a>
    </a>
  </div>
  <div class="py-8 text-center">
    <div class="">
      <div class="w-auto mx-auto mb-10 -mt-10">
        <div class="hidden sm:block">
          <nav class="flex flex-auto space-x-4 justify-center my-4 w-auto" aria-label="Tabs">
            <a v-for="(network) in ['ropsten', 'rinkeby', 'mainnet']" href="#" :key="network" @click="currentNetwork = network" :class="{'bg-gray-200': currentNetwork === network,
            'text-gray-800': currentNetwork === network}"
               class="text-gray-600 hover:opacity-1/2 px-3 py-2 font-medium text-sm rounded-md">
              {{ network }}
            </a>
          </nav>
        </div>
      </div>
      <div class="relative inline-flex flex-col justify-center max-w-content mx-auto">
        <span class="text-sm font-semibold text-indigo-600 uppercase tracking-wide absolute top-0 right-0 transform translate-x-20">{{ currentNetwork }}</span>
        <h1 class="mt-2 text-4xl font-extrabold text-gray-900 tracking-tight sm:text-5xl">Unset CPK</h1>
      </div>
      <p class="mt-2 text-base text-gray-500">This tool allows you to unset zkSync's CPK on testnets </p>
      <div class="mt-6">
        <div class="border-1 inline-flex border-indigo-700 rounded bg-gray-100 py-2 px-4 flex-auto justify-between items-center space-x-3" v-if="loggedIn">
          <h2 class="text-lg text-base p-0 m-0">{{ this.address }}</h2>
          <a :href="zkScanLink" target="_blank"
             class="inline-flex m-0 items-center px-2.5 py-1.5 border border-transparent text-xs font-medium rounded shadow-sm text-white bg-indigo-600 hover:bg-indigo-900"
             v-if="zkScanLink">Open zkScan
            <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd"/>
            </svg>
          </a>
          <a href="#" @click="reset"
             class="inline-flex m-0 items-center px-2.5 py-1.5 border border-transparent text-xs font-medium rounded shadow-xs text-indigo-700 hover:bg-indigo-200 border border-indigo-600">
            Logout
          </a>
        </div>
        <button v-else :disabled="loginInProgress" @click="connect" type="button"
                class="overflow-visible justify-center items-center py-2 px-5 my-8 mx-auto text-xl font-normal leading-normal text-center text-white normal-case align-middle bg-indigo-800 rounded border border-indigo-800 border-solid cursor-pointer select-none box-border whitespace-no-wrap"
                style="transition: background-color 0.21s ease 0s, border-color 0.21s ease 0s, color 0.21s ease 0s;">
          <template v-if="loginInProgress">
            <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor"
                    d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
            connecting...
          </template>
          <template v-else>
            Connect your wallet
          </template>
        </button>
      </div>
    </div>
  </div>
  <div class="w-2/3 flow-root mx-auto" v-if="logs.length > 0">
    <p class="text-sm font-semibold text-indigo-600 mb-4 uppercase tracking-wide">Log board</p>
    <ul role="list" class="-mb-8" id="logs-list">
      <li v-for="oneLog in logs" :key="oneLog.time" :class="{'bg-red-200': oneLog.severity === 'error','bg-yellow-200': oneLog.severity === 'warning'}" class="pr-4">
        <div class="relative pb-8">
          <span class="absolute top-4 left-4 -ml-px h-full w-0.5 bg-gray-200 verticalLine" aria-hidden="true"></span>
          <div class="relative flex space-x-3">
            <div>
              <span class="px-3 py-1 rounded font-bold text-xs bg-gray-400 flex items-center justify-center ring-8 ring-white" :class="{'bg-yellow-500': oneLog.severity ===
              'warning',
                   'bg-red-700': oneLog.severity === 'error', 'text-white': oneLog.severity !== 'log'}">{{ oneLog.severity }}</span>
            </div>
            <div class="min-w-0 flex-1 pt-1.5 flex justify-between space-x-2 overflow-hidden">
              <div class="text-sm text-gray-500 pl-2">{{ oneLog.text }}</div>
              <div class="text-right text-sm whitespace-nowrap text-gray-500">
                <time>{{ oneLog.time.toLocaleTimeString() }}</time>
              </div>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import WalletConnectProvider from "@walletconnect/web3-provider";
import Web3Modal from "web3modal";
import { Web3Provider } from "@ethersproject/providers";
import { getDefaultProvider, Signer as zkSigner, Wallet as zkWallet } from "zksync";

export default {
  computed: {
    zkScanLink () {
      return this.loggedIn ? `https://${this.currentNetwork === "mainnet" ? "" : this.currentNetwork + "."}zkscan.io/explorer/accounts/${this.address}` : undefined;
    },
    loggedIn () {
      return this.address;
    },
    apiUrl () {
      return this.currentNetwork;
    }
  },
  data () {
    return {
      dropdownOpen: false,
      currentNetwork: 'ropsten',
      loginInProgress: false,
      address: "",
      logs: [] as unknown[],
      isLoading: false as boolean
    };
  },
  mounted () {
    const storedNetwork = window.localStorage.getItem("zksync-tool-locker");
    if (storedNetwork){
      this.currentNetwork = storedNetwork;
    }
  },
  watch: {
    currentNetwork(value){
      console.log(value);
      window.localStorage.setItem("zksync-tool-locker", value)
    }
  },
  methods: {
    recordLog (message: string, severity: "log" | "warning" | "error" = "log") {
      this.logs.push({
        text: message,
        severity,
        time: new Date()
      });
      this.$nextTick(() => {
        if (severity !== "error") {
          window.scrollTo(0, document.body.scrollHeight);
        }
      });
    },
    async connect () {
      this.reset();
      try {
        const providerOptions = {
          walletconnect: {
            package: WalletConnectProvider, // required
            options: {
              infuraId: "b818c25e42c049faa539560425a18a4e" // required
            }
          }
        };

        const web3Modal = new Web3Modal({
          network: this.currentNetwork, // optional
          providerOptions // required
        });

        this.recordLog("Awaiting provider...");

        this.loginInProgress = true;

        const provider = await web3Modal.connect();

        this.recordLog("Provider received.");

        const web3Provider = new Web3Provider(provider, this.currentNetwork);

        this.recordLog("Getting ETH Signer...");

        const ethSigner = await web3Provider.getSigner();

        this.recordLog("Trying to sign “hello-world” message...");

        this.recordLog("Signing results: " + (await ethSigner.signMessage("hello-world")));

        this.recordLog("Getting zkProvider...");

        const zksyncProvider = await getDefaultProvider(this.currentNetwork, "HTTP");

        this.recordLog("Provider received");

        this.recordLog("Creating no-keys zkWallet...");

        const wallet = await zkWallet.fromEthSignerNoKeys(ethSigner, zksyncProvider);

        wallet.ethSignerType = {
          verificationMethod: "ERC-1271",
          // Indicates if signer adds `\x19Ethereum Signed Message\n${msg.length}` prefix before signing message.
          // i.e. if false, we should add this prefix manually before asking to sign message
          isSignedMsgPrefixed: true
        };

        this.address = wallet.address();

        this.loginInProgress = false;

        this.recordLog("zkWallet created and configured with ERC-1271 signer type");

        this.recordLog("Replacing signer with seed-based...");

        wallet.signer = await zkSigner.fromSeed(new Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3,
          4,
          5, 6, 7, 8, 9]));

        this.recordLog("zkWallet Signer replaced!");

        this.recordLog("Checking if L2-account exists...");

        const accountId = await wallet.getAccountId();

        if (typeof accountId !== "number") {
          throw Error("It is required to have a history of balances on the account to deactivate CPK");
        }

        this.recordLog("Account exists. ID: " + accountId);

        this.recordLog("Checking if the signing key is set...");

        const isCPKSet = await wallet.isSigningKeySet();

        this.recordLog("CPK is " + (isCPKSet || "not") + " set", isCPKSet ? "log" : "warning");

        this.recordLog("Signing CPK...");

        const tx = await wallet.onchainAuthSigningKey();

        this.recordLog("TNX created successfully. Hash: " + tx.hash);

        this.recordLog("Waiting for the confirmations...");

        await tx.wait();

        this.recordLog("Contract Receipt received");

        this.recordLog("Setting signing key...");

        //
        // console.log("Transaction w/t hash: " + signingTxn.txHash + " has state " + signingTxn.state + " Hash:" + signingTxn.txHash);

        const signingTxn = await wallet.setSigningKey({ feeToken: "ETH", ethAuthType: "Onchain" });

        this.recordLog("Signing key set! Hash: " + signingTxn.txHash);

        this.recordLog("See in block explorer: https://" + (this.currentNetwork === "mainnet" ? "" : this.currentNetwork + ".") + "zkscan.io/explorer/transactions/" + signingTxn.txHash);

        this.recordLog("awaiting tx receipts...");

        const receipt = await signingTxn.awaitReceipt();

        if (receipt.failReason !== undefined) {
          throw Error(receipt.failReason);
        }

        this.recordLog("Success! Block nr: " + receipt.block.blockNumber);

        this.recordLog("ALL DONE! Thanks!");

        return;
      } catch (err) {
        this.reset();
        this.recordLog(err?.message || err as string, "error");
      }
    },
    reset (): void {
      this.loginInProgress = false;
      this.address = null;
      this.recordLog("Resetting all");
    }
  }
};
</script>

<style lang="css">
.logoLetter {
  fill: #11142b;
}

body {
  margin: 0;
  padding: 0;
}

h1, h2 {
  color: rgb(36, 57, 85);
  display: block;
  font: 700 30px/45px "Fira Sans", sans-serif;
  height: 45px;
  text-align: center;
}

h2 {
  height: 30px;
  font-size: 20px;
  line-height: 30px;
  margin: 20px auto;
  font-weight: 500;
}

button {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 7px 12px 7px 7px;
  width: fit-content;
  box-shadow: 0 2px 4px rgba(0, 0, 0, .1);
  appearance: none;
  border-radius: 4px;
  border-image-repeat: stretch;
  border-image-source: none;
  border: 0 none rgb(255, 255, 255);
  box-sizing: border-box;
  color: rgb(255, 255, 255);
  font: 400 16px/22px "Fira Sans", sans-serif;
  margin: 20px 10px;
  min-width: 200px;
  outline: rgb(255, 255, 255) none 0;
  text-align: center;
  text-indent: 0;
  text-rendering: auto;
  text-shadow: none;
  text-transform: none;
  transition: opacity .2s ease;
  white-space: nowrap;
  will-change: opacity;
  word-spacing: 0;
  writing-mode: horizontal-tb;
  cursor: pointer;
  opacity: .7;
}

button:hover {
  opacity: 1;
}

#logs-list li:last-child .verticalLine {
  display: none !important;
}
</style>
