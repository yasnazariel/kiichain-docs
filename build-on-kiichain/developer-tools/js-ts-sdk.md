---
description: An SDK written in Javascript/Typescript for KiiChain
---

# JS/TS SDK

**Note: This project is still under development so future changes will be made.**&#x20;

### Important Links

* [JS/TS SDK repository](https://github.com/KiiChain/kiijs-sdk)

## Kiijs-SDK

A JS/TS library for interacting with KiiChain and other Cosmos-based blockchain networks. This repo will not be 100% finalized until mainnet launch, therefore, changes could be made.&#x20;

### Getting Started

`kiijs` is a library written in TypeScript used for interacting with KiiChain. The library provides methods to conveniently send transactions, query data, and manage wallets. The library is implemented based on gRPC-web protocol which sends HTTP/1.5 or HTTP/2 requests to a gRPC proxy server, before serving them as HTTP/2 to gRPC server.

The library supports both Node.js and browsers.

### Installation

#### Install with npm

```sh
npm install kiijs
```

#### Install with yarn

```sh
yarn add kiijs
```

### Getting Started

Below is a simple example for querying an account's balances:

```typescript
import {KiiStargateQueryClient} from "../kiijs/client";

async function main() {

  // connect to Kiichain test network using rpc
  const rpcEndpoint = "https://a.testnet.kiivalidator.com:26658/";
  const client = await KiiStargateQueryClient.connect(
    rpcEndpoint
  );
  
  // show all coin balances
  const address = "kii1s0jekzmfy3ejmf75lh0xfc2zl3958lfk8gqtws";
  const balance = await client.getAllBalances(address);
  console.log('balance', balance);
}
```

### Documentation

The full documentation and repo can be found [here](https://github.com/KiiChain/kiijs-sdk/blob/main/README.md).

### Examples

Under the [`examples`](https://github.com/KiiChain/kiijs-sdk/tree/main/example) directory, you can find examples of basic ledger interactions using `kiijs`, such as transferring tokens, staking, and deploying.

### Contributing

All contributions are very welcome! Remember, contribution is not only PRs and code, but any help with docs or helping other developers solve their issues are very appreciated!

Read below to learn how you can take part in the KiiPy project.

#### Code of Conduct

Please be sure to read and follow our [Code of Conduct](https://github.com/KiiChain/kiijs-sdk/blob/main/CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

#### Contribution Guidelines

Read our [contribution guidelines](https://github.com/KiiChain/kiijs-sdk/blob/main/CONTRIBUTING.md) to learn about our issue and pull request submission processes, coding rules, and more.

#### Issues, Questions and Discussions

We use [GitHub Issues](https://github.com/KiiChain/kiijs-sdk/issues) for tracking requests and bugs, for general questions and discussion.

### License

The KiiPy project is licensed under [Apache License 2.0](https://github.com/KiiChain/kiijs-sdk/blob/main/LICENSE).
