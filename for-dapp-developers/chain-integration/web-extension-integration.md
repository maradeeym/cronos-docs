# Wallet integrations

## Overview

Cronos chain is supported by the following self-custodial wallets:

* Crypto.com DeFi Wallet.
* Rabby (rabby.io)
* MetaMask (requires custom network configuration) (metamask.io).
* Trust Wallet.
* and more than 30 other wallets (you can see a more complete list of dev tools [here](https://crofam.me/devtools)).

Crypto.com DeFi Wallet, Trust Wallet and MetaMask have mobile apps that include in-app dApp browsers. Users can access dApps on the go via these in-app browsers. We recommend that all dApp developers integrate with these 3 wallets at least, and more if possible.

## Basic tutorial

[Follow this link](web3-wallet.md) for a basic example on how to implement the main wallet connection methods available to Cronos dApp developers.

## Crypto.com DeFi Wallet

#### &#x20;A non-custodial wallet to store, earn, and grow your crypto

[Crypto.com DeFi Wallet](https://crypto.com/defi-wallet) is a non-custodial wallet that gives users full control of their crypto and private keys. Private keys are encrypted locally on the user’s mobile phone, and protected by Biometric Authentication and 2-Factor Authentication.&#x20;

If you are a dApp developer, integration with the Crypto.com DeFi Wallet is the best way to deliver a smooth user experience to more than 50 million Crypto.com customers.

Users will be able to login with your dApp in several ways:

* On Mobile, they can visit your dApp and connect to it via the in-app browser of the Crypto.com DeFi Wallet iOS or Android apps.
* On Desktop, they can install the Crypto.com Wallet Extension from the Chrome extension store into their Chrome, Edge or Brave browser. The extension can be connected to the Crypto.com DeFi Wallet mobile app (in which case the user will need to confirm each transaction on their mobile phone), or alternatively it can work as a standalone extension entirely in the browser.
* Finally, on Desktop too, the Crypto.com DeFi Wallet is available as a standalone app.&#x20;

To get your dApp listed on the dApp section of Crypto.com DeFi Wallet, the steps are as below:&#x20;

* Make sure your dApp completes the integration of the Crypto.com Wallet  Extension SDK and the wallet connection is working (see below for details)
* Provide your dApp details in the [Submission Form](https://crypto-com.typeform.com/to/bRvudlYV)
* Crypto.com DeFi Wallet Team reviews submission with stakeholders
* Crypto.com DeFi Wallet Team may proceesd with the dApp listing

As a developer, if you would like to offer all the mobile and desktop connection options provided by the Crypto.com DeFi Wallet, the first step is to integrate your dApp with the Crypto.com Wallet  Extension.

Once the Wallet Extension is working, all the other connection methods should start working as well, even on mobile, since they are supported by the same SDKs.

The Crypto.com Wallet Extension currently supports the following networks:

{% tabs %}
{% tab title="Mainnet" %}
* Cronos
* Cronos POS Chain
* Ethereum
* Bitcoin
* BNB Smart Chain
* Polygon
* Avalanche-C
* Cosmos
* Fantom
* Arbitrum
* Optimism
* Gnosis
* Aptos
* All other EVM-compatible networks (manual configuration)
{% endtab %}

{% tab title="Testnet" %}
* Cronos Testnet
* Goerli Testnet
* Scroll Alpha Testnet
* Aptos Devnet
* Aptos Testnet
{% endtab %}
{% endtabs %}

The official repository and documentation of Crypto.com Wallet Extension are available at: [https://github.com/crypto-com/deficonnect-monorepo](https://github.com/crypto-com/deficonnect-monorepo).

**For most dApp developers,** the best way to integrate the Crypto.com Wallet Extension is to develop your application's front-end in React and to use the DeFiWeb3Connector object which is provided by the `"@deficonnect/web3-connector"` npm package as documented here: [https://github.com/crypto-com/deficonnect-monorepo/tree/develop/packages/web3-connector](https://github.com/crypto-com/deficonnect-monorepo/tree/develop/packages/web3-connector).

Once the connector is activated, your dApp can retrieve the provider using `getProvider()` and subsequently use it via a common Web3 SDK like ethers.js.

**Some developers** may need to dig deeper into the documentation, for example if they are not using React or need more customization. In this case, please refer to:

* Github: [https://github.com/crypto-com/deficonnect-monorepo](https://github.com/crypto-com/deficonnect-monorepo)
* Document: [https://github.com/crypto-com/deficonnect-monorepo/wiki/Chrome-Extension-Wallet-Integration ](https://github.com/crypto-com/deficonnect-monorepo/wiki/Chrome-Extension-Wallet-Integration)

