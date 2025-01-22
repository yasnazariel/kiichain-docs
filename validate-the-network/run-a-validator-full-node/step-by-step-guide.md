---
description: Onboarding for validators
---

# Step-by-Step Guide

It's always nice to see new users onboarding into the Testnet Oro.

This will guide you through the process of running your own node and becoming a validator.

## Install

`kiichaind` is the command-line interface (CLI) for interacting with the Kiichain blockchain. This section covers the installation of the necessary binaries to run a Kiichain node.

### Requirements

* Golang v1.22 linux/amd64
* Linux build-essential

### Binary installation

To install Kiichain, download the pre-built binaries:

```bash
git clone https://github.com/KiiChain/kiichain.git
cd kiichain3
make install
```

Verify the installation by checking the version of kiichaind:

```bash
kiichaind version
```

## Joining the Testnet

To join the Testnet Oro, you must have the daemon `kiichaind` installed in your machine.

### Recommended configuration

For optimal performance, we recommend:

* 16 vCPU x86\_64
* 64 GB RAM
* 1 TB NVME SSD

### Quick bootstrap

The way best of preparing a node is using our scripts:

* **Join Testnet Oro Script**: Use this script to quickly bootstrap a full node.

```bash
curl -O https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/master/testnet_oro/join_oro.sh
chmod +x join_oro.sh
./join_oro.sh
```

* **Join Testnet with Cosmosvisor Script**: Use this script to set up a full node with Cosmosvisor for automated upgrades

```bash
curl -O https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/master/testnet_oro/join_oro_cv.sh
chmod +x join_oro_cv.sh
./join_oro_cv.sh
```

### Running your node

Prepare your system by backing up and removing old configurations:

```bash
# Backup old configuration
cp -r $HOME/.kiichain3 $HOME/.kiichain3-bk
# Clean any old configuration
rm -r $HOME/.kiichain3
```

Connect to the testnet with the following commands:

```bash
# Variables used during the configuration
PERSISTENT_PEERS="5b6aa55124c0fd28e47d7da091a69973964a9fe1@uno.sentry.testnet.v3.kiivalidator.com:26656,5e6b283c8879e8d1b0866bda20949f9886aff967@dos.sentry.testnet.v3.kiivalidator.com:26656"
CHAIN_ID=kiichain3
NODE_HOME=~/.kiichain3
NODE_MONIKER=testnet_oro
GENESIS_URL=https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/main/testnet_oro/genesis.json

# Initialize the chain
kiichaind init $NODE_MONIKER --chain-id $CHAIN_ID --home $NODE_HOME

# Set the PERSISTENT_PEERS
sed -i -e "/persistent_peers =/ s^= .*^= \"$PERSISTENT_PEERS\"^" $NODE_HOME/config/config.toml

# Set the block time to 3 seconds
sed -i 's/unsafe-propose-timeout-override = .*/unsafe-propose-timeout-override = "3s"/g' $NODE_HOME/config/config.toml
sed -i 's/unsafe-propose-timeout-delta-override = .*/unsafe-propose-timeout-delta-override = "500ms"/g' $NODE_HOME/config/config.toml
sed -i 's/unsafe-vote-timeout-override = .*/unsafe-vote-timeout-override = "1s"/g' $NODE_HOME/config/config.toml
sed -i 's/unsafe-vote-timeout-delta-override = .*/unsafe-vote-timeout-delta-override = "500ms"/g' $NODE_HOME/config/config.toml
sed -i 's/unsafe-commit-timeout-override = .*/unsafe-commit-timeout-override = "3s"/g' $NODE_HOME/config/config.toml

# Set the genesis
wget $GENESIS_URL -O genesis.json
mv genesis.json $NODE_HOME/config/genesis.json

# Start the chain
kiichaind start --home $NODE_HOME
```

**(Optional but recommended)**: Before running the chain you can also check the SHA256:

```bash
sha256sum $NODE_HOME/config/genesis.json
```

The expected SHA256 checksum is: `e22442f19149db7658bcf777d086b52b38d834ea17010c313cd8aece137b647a`

\==NOTE==:

* This configuration runs a full node. For validators, update the configuration accordingly.

```bash
# Set the node as validator
sed -i 's/mode = "full"/mode = "validator"/g' $NODE_HOME/config/config.toml
```

### Configure state sync

State sync significantly reduces the time required to synchronize a node by downloading and verifying state data from trusted peers rather than replaying every historical block. This is particularly beneficial for nodes joining the network late or recovering from a significant downtime.

Follow these steps to configure state sync for your Kiichain node:

1. **Set Trust Height Delta and Fetch Block Information**

Define a height delta and retrieve the latest block height and block hash from the primary RPC endpoint.

```shellscript
# Configure state-sync
TRUST_HEIGHT_DELTA=500
LATEST_HEIGHT=$(curl -s https://rpc.uno.sentry.testnet.v3.kiivalidator.com/block | jq -r ".block.header.height")
if [[ "$LATEST_HEIGHT" -gt "$TRUST_HEIGHT_DELTA" ]]; then
SYNC_BLOCK_HEIGHT=$(($LATEST_HEIGHT - $TRUST_HEIGHT_DELTA))
else
SYNC_BLOCK_HEIGHT=$LATEST_HEIGHT
fi

# Get the sync block hash
SYNC_BLOCK_HASH=$(curl -s "https://rpc.uno.sentry.testnet.v3.kiivalidator.com/block?height=$SYNC_BLOCK_HEIGHT" | jq -r ".block_id.hash")
```



2. Enable State Sync in Configuration

Modify the `config.toml` file to enable state sync and set the required parameters.

```bash
sed -i.bak -e "s|^enable *=.*|enable = true|" $NODE_HOME/config/config.toml
sed -i.bak -e "s|^rpc-servers *=.*|rpc-servers = \"https://rpc.uno.sentry.testnet.v3.kiivalidator.com,https://rpc.dos.sentry.testnet.v3.kiivalidator.com\"|" $NODE_HOME/config/config.toml
sed -i.bak -e "s|^db-sync-enable *=.*|db-sync-enable = false|" $NODE_HOME/config/config.toml
sed -i.bak -e "s|^trust-height *=.*|trust-height = $SYNC_BLOCK_HEIGHT|" $NODE_HOME/config/config.toml
sed -i.bak -e "s|^trust-hash *=.*|trust-hash = \"$SYNC_BLOCK_HASH\"|" $NODE_HOME/config/config.toml
```

## Becoming a validator

Validators are the main responsible of validating and committing blocks. The main advantages of becoming a validator are:

* Fees: Each transaction has fees, and validators are the main entry points of fee distribution. And due to his help on decentralization, part of the fee is exclusive for validators.

### Creating a validator

1. **Key creation**

To create a validator, you first must have a key available for transactions. A new key can be created with:

```bash
kiichaind keys add $VALIDATOR_KEY_NAME
```

You will get an output such as:

```
- name: asd
  type: local
  address: kii1507zhg2k7al477zqarzru7n4566lvcp9xnsxll
  evm_address: ""
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"Ak5kTpx4OIzXYWAOPjEVNFnn/9O+6BUgSbYCYpnUpRU5"}'
  mnemonic: ""

**Important** write this mnemonic phrase in a safe place.
It is the only way to recover your account if you ever forget your password.

invite hollow salon dutch since six embrace squeeze label other pass bean size public lazy scissors spare blood safe nothing rapid list ritual license
```

2. **Transfer funds**

Ensure your account has sufficient funds for fees and self-delegation.

3. **Create the validator**

A validator will be created based on your consensus public key. You can check your current public key using:

```bash
kiichaind tendermint show-validator
```

To create a validator you can use the following command:

```bash
# Basic chain information
CHAIN_ID=kiichain3

# Define the validator information
MONIKER=<my-moniker>
AMOUNT=1000000000ukii # 1000 kii as self delegation
COMMISSION_MAX_CHANGE_RATE=0.1
COMMISSION_MAX_RATE=0.1
COMMISSION_RATE=0.1
MIN_SELF_DELEGATION_AMOUNT=1000000000

kiichaind tx staking create-validator \
  --amount=$AMOUNTukii \
  --pubkey=$(kiichaind tendermint show-validator) \
  --moniker=$MONIKER \
  --chain-id=$CHAIN_ID \
  --commission-rate=$COMMISSION_RATE \
  --commission-max-rate=$COMMISSION_MAX_RATE \
  --commission-max-change-rate=$COMMISSION_MAX_CHANGE_RATE \
  --min-self-delegation=$MIN_SELF_DELEGATION_AMOUNT \
  --gas="auto" \
  --gas-prices="0.01ukii" \
  --from=$VALIDATOR_KEY_NAME
```

\==NOTE==:

* The transaction must be done on the machine running the node
  * An additional flag `--node` can be passed to point to an available RPC node
* Further instruction on how to run a validator can be found at [Running a Validator](https://hub.cosmos.network/validators/validator-setup)

### Cosmosvisor

Cosmosvisor is a process manager for handling chain upgrades. It enables low maintenance and automatic updates for nodes.

* If an upgrade is scheduled, cosmosvisor has the capability of automatically downloading binaries and restarting any Kiichain processes
* This gives the node low maintenance and auto updates capabilities

More information about cosmovision can be found at [Cosmosvisor Quick Start](https://docs.cosmos.network/v0.45/run-node/cosmovisor.html)

### Node Architecture for validators

Further instruction on how to build a great node architecture can be found on:

* [Playbook For Cosmos Validators: Node Architecture Choices](https://medium.com/@kidinamoto/tech-choices-for-cosmos-validators-27c7242061ea)

## References

* [Running a Validator](https://hub.cosmos.network/validators/validator-setup)
* [Playbook For Cosmos Validators: Node Architecture Choices](https://medium.com/@kidinamoto/tech-choices-for-cosmos-validators-27c7242061ea)
* [Cosmosvisor Quick Start](https://docs.cosmos.network/v0.45/run-node/cosmovisor.html)
* [Join Testcorn](https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/main/testnet_oro/join_oro.sh)
* [Join Testcorn CV](https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/main/testnet_oro/join_oro_cv.sh)
