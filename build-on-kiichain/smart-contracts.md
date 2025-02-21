---
description: How to deploy smart contracts
---

# Smart contracts

Kiichain supports **natively supports both CosmWasm and EVM smart contracts.** Developers can choose between any of the two to create amazing dApps.

***

## Working with Cosmwasm

#### Prerequisites

*   Install Rust and CosmWasm toolchain:

    ```bash
    rustup default stable
    rustup target add wasm32-unknown-unknown
    cargo install cargo-generate --features vendored-openssl
    cargo install cargo-run-script
    ```
*   Create a new CosmWasm contract:

    ```bash
    cargo generate --git https://github.com/CosmWasm/cosmwasm-template.git --name my-contract
    cd my-contract
    ```
*   Compile the contract:

    ```bash
    cargo wasm
    cargo schema
    ```

#### Upload and Instantiate the Contract

1.  **Store the Contract**

    ```bash
    kiichaind wasmd tx wasm store artifacts/my_contract.wasm --from my-key --gas auto --gas-adjustment 1.2 --node <KIICHAIN_NODE> --chain-id <KIICHAIN_CHAIN_ID>
    ```
2.  **Instantiate the Contract**

    ```bash
    kiichaind wasmd tx wasm instantiate <CONTRACT_CODE_ID> '{}' --from my-key --label "My Contract" --gas auto --gas-adjustment 1.2 --node <KIICHAIN_NODE> --chain-id <KIICHAIN_CHAIN_ID>
    ```
3.  **Execute the Contract**

    ```bash
    kiichaind wasmd tx wasm execute <CONTRACT_ADDRESS> '{"your_method": {}}' --from my-key --gas auto --gas-adjustment 1.2 --node <KIICHAIN_NODE> --chain-id <KIICHAIN_CHAIN_ID>
    ```

***

## Working with EVM

#### Prerequisites

*   Install **Node.js** and **Hardhat**:

    ```bash
    npm install -g hardhat
    mkdir my-evm-contract && cd my-evm-contract
    npx hardhat
    ```
*   Install dependencies:

    ```bash
    npm install --save-dev @nomicfoundation/hardhat-toolbox
    ```

#### Write and Compile the Smart Contract

1.  Create a Solidity file (`MyContract.sol`) in `contracts/`:

    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.19;

    contract MyContract {
        string public message;

        constructor(string memory _message) {
            message = _message;
        }

        function setMessage(string memory _newMessage) public {
            message = _newMessage;
        }
    }
    ```
2.  Compile the contract:

    ```bash
    npx hardhat compile
    ```

#### Deploy the Smart Contract

1.  Create a deployment script (`scripts/deploy.js`):

    ```javascript
    const hre = require("hardhat");

    async function main() {
        const MyContract = await hre.ethers.getContractFactory("MyContract");
        const contract = await MyContract.deploy("Hello, Kiichain!");
        await contract.deployed();
        console.log("Contract deployed at:", contract.address);
    }

    main().catch((error) => {
        console.error(error);
        process.exitCode = 1;
    });
    ```
2.  Deploy to Kiichain:

    ```bash
    npx hardhat run scripts/deploy.js --network kiichain
    ```

#### Interact with the Deployed Contract

*   **Using Hardhat Console**:

    ```bash
    npx hardhat console --network kiichain
    ```

    ```javascript
    const contract = await ethers.getContractAt("MyContract", "<DEPLOYED_CONTRACT_ADDRESS>");
    await contract.setMessage("New Message");
    ```

***

## References

* **CosmWasm Documentation:** [CosmWasm Docs](https://docs.cosmwasm.com/)
* **Ethereum Hardhat Guide:** [Hardhat Docs](https://hardhat.org/getting-started)
