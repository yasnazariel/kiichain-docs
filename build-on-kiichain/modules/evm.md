# EVM

The **EVM Module** enables full Ethereum Virtual Machine compatibility within Kiichain, allowing developers to deploy and interact with Ethereum smart contracts using familiar tools like MetaMask, Remix, Hardhat, and Web3 libraries.

This module is built on top of the  [Cosmos EVM implementation](https://github.com/cosmos/evm).

## Overview

The `evm` module provides:

* EVM Execution Environment within Cosmos-SDK
* Support for Ethereum JSON-RPC APIs
* Full Solidity smart contract compatibility

## Available Messages and Transactions



The EVM module provides several messages and transactions that users and developers can utilize:​

### Ethereum Transactions

* **Submit Ethereum Transactions**: Users can submit Ethereum-formatted transactions (`MsgEthereumTx`) to Kiichain, which are processed by the EVM module.​

### CLI Commands

Kiichain offers command-line interface (CLI) commands for interacting with the EVM module:​

* Query Smart Contract Code:

```
kiichaind query evm code [address]
# Example:
kiichaind query evm code 0x7bf7b17da59880d9bcca24915679668db75f9397
```

* Query Storage:

```
kiichaind query evm storage [address] [key] [flags]
# Example:
kiichaind query evm storage 0x0f54f47bf9b8e317b214ccd6a7c3e38b893cd7f0 0 --height 0
```

* Submit Raw Ethereum Transaction:

```
kiichaind tx evm raw [tx_hex]
# Example:
kiichaind tx evm raw 0xf9ff74c86aefeb5f6019d77280bbb44fb695b4d45cfe97e6eed7acd62905f4a85034d5c68ed25a2e7a8eeb9baf1b84
```

### JSON-RPC Support

Kiichain's EVM module exposes standard Ethereum JSON-RPC endpoints, allowing developers to interact with the blockchain using familiar methods:​

* **eth\_sendTransaction**: Send a transaction
* **eth\_call**: Call a smart contract function without making a state-changing transaction
* **eth\_estimateGas**: Estimate the gas required for a transaction
* **debug\_traceTransaction**: Trace the execution of a transaction for debugging purposes

And other general EVM JSON-RPC calls.

## FeeMarket Module

The `x/feemarket` module implements a dynamic fee mechanism inspired by Ethereum's EIP-1559, enhancing transaction fee predictability and network efficiency.​

### Key Concepts

* **Base Fee**: A global, per-block fee that adjusts based on network demand. It increases when blocks are above the gas target and decreases when below. Unlike Ethereum, where the base fee is burned, Kiichain allocates it for regular Cosmos SDK fee distribution.​
* **Priority Tip**: An optional fee that users can include to prioritize their transactions. While Cosmos SDK v0.46 lacks native transaction prioritization, this tip can still influence transaction inclusion.
* **Effective Gas Price**: Determined by the minimum of `(baseFee + priorityTip)` and `gasFeeCap`, ensuring users don't overpay for transactions.
* **Minimum Gas Prices**: Validators can set local minimum gas prices, and a global minimum can be established via governance. Transactions below these thresholds are discarded, mitigating spam

This module ensures a more stable and predictable fee structure, benefiting both users and validators.

## ERC20

The `x/erc20` module facilitates seamless, trustless conversion between Cosmos-native tokens and ERC-20 tokens, bridging the gap between the Cosmos and Ethereum ecosystems.

### Key Concepts

* **Bidirectional Conversion**: Users can convert native Cosmos `sdk.Coins` to ERC-20 tokens and vice versa, enabling interoperability between different blockchain applications.
* **Token Pair Registration**: Mappings between Cosmos denominations and ERC-20 contract addresses, known as `TokenPairs`, are managed via governance proposals. This ensures controlled and secure token conversions.
* Use Cases
  * Utilize Cosmos assets (e.g., ATOM, OSMO) in Ethereum-based DeFi protocols.
  * Transfer ERC-20 tokens to Kiichain for use within the Cosmos ecosystem.
  * Enable applications that require ERC-20 standard tokens while leveraging Cosmos SDK features.

By supporting ERC-20 token standards, Kiichain enhances its interoperability, allowing for a broader range of decentralized applications and services.​
