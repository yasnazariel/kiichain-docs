---
description: Everything you need to know  about our Testnet Oro
---

# Testnet Oro

KiiChain is a peer-to-peer decentralized EVM-compatible network built with the Cosmos SDK.  The public testnet is called KiiChain Testnet Oro.

Testnet Oro is the permanent testnet with smart contract functionality and EVM compatibility. All Hackathons, Builds, Airdrops, and test deployments should be done on this network.

## Source code

The source code for the Testnet Oro can be found at:

<!-- markdown-link-check-disable -->
* [Kiichain](https://github.com/KiiChain/kiichain)

## Endpoints

Testnet Oro has the following endpoints open for development purposes:

**Sentry #1:**

* **RPC:** [https://rpc.uno.sentry.testnet.v3.kiivalidator.com/](https://rpc.dos.sentry.testnet.v3.kiivalidator.com/)
* **Rest (LCD):** [https://lcd.uno.sentry.testnet.v3.kiivalidator.com/](https://lcd.dos.sentry.testnet.v3.kiivalidator.com/)
* **JSON-RPC (EVM):** [https://json-rpc.uno.sentry.testnet.v3.kiivalidator.com/](https://json-rpc.dos.sentry.testnet.v3.kiivalidator.com/)
* **Peer:** 5b6aa55124c0fd28e47d7da091a69973964a9fe1@uno.sentry.testnet.v3.kiivalidator.com:26656

**Sentry #2:**

* **RPC:** [https://rpc.dos.sentry.testnet.v3.kiivalidator.com/](https://rpc.dos.sentry.testnet.v3.kiivalidator.com/)
* **Rest (LCD):** [https://lcd.dos.sentry.testnet.v3.kiivalidator.com/](https://lcd.dos.sentry.testnet.v3.kiivalidator.com/)
* **JSON-RPC (EVM):** [https://json-rpc.dos.sentry.testnet.v3.kiivalidator.com/](https://json-rpc.dos.sentry.testnet.v3.kiivalidator.com/)
* **Peer:** 5e6b283c8879e8d1b0866bda20949f9886aff967@dos.sentry.testnet.v3.kiivalidator.com:26656

Currently, there are no seed nodes or persistent peers available to the public.

## Chain information

Here you can find further information about Testnet Oro:

* **Chain ID:** `kiichain`
* **Total Supply:** `1.8b Kii`
* **Token Denom:** `ukii`
* **EVM Chain ID:** `1336`
* **Bench32 Prefix:** `kii`

## Faucet

You can get tokens to our Testnet Oro by using our Explorer app:

* [KiiChain Explorer Faucet](https://app.kiichain.io/wallet/accounts)

Our through our Discord channel:

* [Discord Kiichain Invitation](https://discord.com/invite/kiichain)

More information about how to use our discord Faucet can be found at:

* [Testnet Faucet](developer-tools/testnet-faucet.md)

## Explorer

The testnet Oro also has its own Explorer, it can be found here:

* [Testnet Oro Explorer](https://app.kiichain.io/Testnet%20Oro)

## Developer Tools

You can find guides to the testnet at our [Developer Tools](testnet-oro.md#developer-tools):

* [RWA Protocol](developer-tools/rwa-protocol.md)
* [Deploying a smart contract](developer-tools/deploy-a-smart-contract.md)
* [Deploying a dApp](developer-tools/deploy-a-dapp.md)

## Endpoints

Rest endpoints for the testnet Oro can be found here:

* [Endpoints](endpoints-cosmos/)

## **EVM / CW Addresses**

KiiChain Testnet Oro features a mirrored EVM - CW smart contract module that replicates EVM compatibility. CW addresses are structured in Bech32 format with a distinctive "kii" prefix, characteristic of Cosmos-based chains. EVM addresses are structured with the hexadecimal format akin to Ethereum addresses. This alteration reflects a strategic adaptation to streamline interoperability with Ethereum-based tools and infrastructure, facilitating a seamless transition for developers and users alike.

```
// CosmWasm based addresses
kii123abc...

// EVM based addresses
0x123abc...
```

## **Tokens**&#x20;

Kiichain Testnet Oro introduces a mirrored token system comprising uKII in both ERC and CW token standards. KiiChain is a Cosmos-based blockchain built with the Cosmos SDK, therefore, all functionalities will be based on CW tokens. ERC tokens are mirrored from the cosmos environment through precompiled smart contracts that give users and builders access to EVM infrastructure.&#x20;

KII serves as the primary utility token within the KiiChain ecosystem, facilitating transactions and powering network operations, notably through the payment of gas fees. Distinguished by its fungibility and interoperability, KII can be seamlessly transferred and utilized across various wallet providers, including popular EVM rpc-based options like MetaMask & Coinbase wallet and cosmos-based wallets like Keplr and Leap. By leveraging KII, users can engage in a diverse array of interactions within the KiiChain network, ranging from simple transactions to more complex smart contract executions, thereby driving the adoption and utility of the native token within the broader blockchain landscape.
