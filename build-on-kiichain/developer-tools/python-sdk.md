---
description: An SDK written in Python for KiiChain
---

# Python SDK

### **Introduction to the SDK**

**Note: This project is still under development so future changes will be made.**&#x20;

### Important Links

* [Python SDK Repository](https://github.com/KiiChain/kiipy-sdk)

## Kiipy-SDK

The Python SDK allows you to build on KiiChain with a predetermined set of coding. You can index, query, and send transactions, as well as access market data for various purposes like analysis, creating indicators, algorithmic trading, strategy backtesting, and bot programming.

This package is ideal for developers, coders, experienced traders, and data scientists who are interested in building on the network.

### **Start here**

Details on how to set up the dev environment can be found in the [development guidelines](https://github.com/KiiBlockchain/kiipy/blob/main/DEVELOPING.md). Using poetry virtual environment is highly encouraged to ensure seamless development.

Notes:

* Items that need to be looked into are marked as `TODO:` in the code and docs.
* Workflows are failing due to usage limits. It's advisable to fix this to ensure code quality. The current workaround is to make sure to run corresponding checks and tests locally.

### Installation

#### Install with pip

```sh
pip install kiipy
```

#### Install from source code

1. Clone the repository

```sh
git clone https://github.com/KiiBlockchain/kiipy.git
cd kiipy
```

2. Install the required dependencies

```sh
poetry install
```

3. Open the virtual environment

```sh
poetry shell
```

### Getting Started

Below is a simple example for querying an account's balances:

```python
from kiipy.aerial.client import LedgerClient, NetworkConfig

# connect to Kii test network using default parameters
ledger_client = LedgerClient(NetworkConfig.kii_testnet())

alice: str = 'kii1pyt53arxkg5t4aww892esskltrf54mg88va98y'
balances = ledger_client.query_bank_all_balances(alice)

# show all coin balances
for coin in balances:
  print(f'{coin.amount}{coin.denom}')
```

### Examples

Under the [`examples`](https://github.com/KiiChain/kiipy-sdk/tree/main/examples) directory, you can find examples of basic ledger interactions using `kiipy`, such as transferring tokens, staking, and deploying.

### Contributing

All contributions are very welcome! Remember, contribution is not only PRs and code, but any help with docs or helping other developers solve their issues are very appreciated!

Read below to learn how you can take part in the KiiPy project.

#### Code of Conduct

Please be sure to read and follow our [Code of Conduct](https://github.com/KiiBlockchain/kiipy/blob/main/CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

#### Contribution Guidelines

Read our [contribution guidelines](https://github.com/KiiBlockchain/kiipy/blob/main/CONTRIBUTING.md) to learn about our issue and pull request submission processes, coding rules, and more.

#### Development Guidelines

Read our [development guidelines](https://github.com/KiiBlockchain/kiipy/blob/main/DEVELOPING.md) to learn about the development processes and workflows.

#### Issues, Questions and Discussions

We use [GitHub Issues](https://github.com/KiiBlockchain/kiipy/issues) for tracking requests and bugs, for general questions and discussion.

### License

The KiiPy project is licensed under [Apache License 2.0](https://github.com/KiiBlockchain/kiipy/blob/main/LICENSE).
