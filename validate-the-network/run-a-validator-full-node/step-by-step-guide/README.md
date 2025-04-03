---
description: Onboarding for validators
---

# Step-by-Step Guide

It's always nice to see new users onboarding into the Testnet Oro.

This will guide you through the process of running your own full node, then [becoming a validator](becoming-a-validator.md) and finally running[ the price feeder](running-the-price-feeder.md)

## Install

`kiichaind` is the command-line interface (CLI) for interacting with the Kiichain blockchain. This section covers the installation of the necessary binaries to run a Kiichain node.

### Requirements

* **Golang version:** `v1.21.x` or `v1.22.x`
* **Build tools:** `build-essential` package (Linux)

{% hint style="warning" %}
Using Golang `v1.23.x` or higher will result in compilation errors. Please ensure you install an appropriate version.
{% endhint %}

### Binary installation

To install Kiichain, download the pre-built binaries:

```bash
git clone https://github.com/KiiChain/kiichain.git
cd kiichain
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

The easiest way to prepare a node is by using our provided scripts.

{% hint style="info" %}
These scripts are designed for systems running **Ubuntu 20.04** or **Ubuntu 22.04**. Ensure your operating system matches this requirement before proceeding.
{% endhint %}

* **Join Testnet Oro Script**: Use this script to bootstrap a full node quickly.

```bash
curl -O https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/main/testnet_oro/join_oro.sh
chmod +x join_oro.sh
./join_oro.sh
```

* **Join Testnet with Cosmosvisor Script**: Use this script to set up a full node with Cosmosvisor for automated upgrades

```bash
curl -O https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/main/testnet_oro/join_oro_cv.sh
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

# Set the persistent-peers
sed -i -e "/persistent-peers =/ s^= .*^= \"$PERSISTENT_PEERS\"^" $NODE_HOME/config/config.toml

# Enable DB
sed -i.bak -e "s|^occ-enabled *=.*|occ-enabled = true|" $NODE_HOME/config/app.toml
sed -i.bak -e "s|^sc-enable *=.*|sc-enable = true|" $NODE_HOME/config/app.toml
sed -i.bak -e "s|^ss-enable *=.*|ss-enable = true|" $NODE_HOME/config/app.toml
sed -i.bak -e 's/^# concurrency-workers = 20$/concurrency-workers = 500/' $NODE_HOME/config/app.toml

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

{% hint style="warning" %}
This configuration runs a full node. For validators, update the configuration accordingly!
{% endhint %}

### Cosmosvisor

Cosmosvisor is a process manager for handling chain upgrades. It enables low maintenance and automatic updates for nodes.

* If an upgrade is scheduled, cosmosvisor has the capability of automatically downloading binaries and restarting any Kiichain processes
* This gives the node low maintenance and auto updates capabilities

A version of our node bootstrapper can install cosmosvisor for you:

```
curl -O https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/main/testnet_oro/join_oro_cv.sh
chmod +x join_oro_cv.sh
./join_oro_cv.sh
```

More information about cosmovision can be found at [Cosmosvisor Quick Start](https://docs.cosmos.network/v0.45/run-node/cosmovisor.html).

#### Preparing cosmosvisor upgrade

First, you need to compile new binaries:

* A new Kiichaind binary must be compiled with the target OS in mind
* Ideally, you should compile all binaries on it’s own machines
* **The build must be done on top of the upgrade tag (E.g. v1.0.1, v2.0.0)**
* Check the section [Binary Installation](./#binary-installation) on how to do it

Make sure that the binary has the correct version with:

```
kiichaind version
```

To add a new upgrade you must run the following command on Cosmovisor:

```
cosmovisor add-upgrade <upgrade-name> <path-to-binary>
```

Where:

* `<upgrade-name>` is the on-chain upgrade name
* `<path-to-binary>` is the full path for the binary

Example:

```
cosmovisor add-upgrade 1.3.0 /home/ubuntu/kiichain/build/kiichaind
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

### Turning your node into an archival node

Newly created nodes have the pruning option configured as default. If you desire to turn your node into an archival node, the following flag must be changed:

1. Go to `$NODE_HOME/config/app.toml`and update the following flag:

```
pruning = "nothing"
```

Other options available as default for pruning are:

* `default`: Keep the recent 362880 blocks and prune is triggered every 10 blocks
* `nothing`: all historic states will be saved, and nothing will be deleted (i.e. archiving node)
* `everything`: all saved states will be deleted, storing only the recent 2 blocks; pruning at every block
* `custom`: allow pruning options to be manually specified through 'pruning-keep-recent' and 'pruning-interval'

### Node Architecture for Validators

Further instructions on how to build a great node architecture can be found on:

* [Playbook For Cosmos Validators: Node Architecture Choices](https://medium.com/@kidinamoto/tech-choices-for-cosmos-validators-27c7242061ea)

## References

* [Running a Validator](https://hub.cosmos.network/main/validators/validator-setup.html)
* [Playbook For Cosmos Validators: Node Architecture Choices](https://medium.com/@kidinamoto/tech-choices-for-cosmos-validators-27c7242061ea)
* [Cosmosvisor Quick Start](https://docs.cosmos.network/v0.45/run-node/cosmovisor.html)
* [Join Testnet Oro](https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/main/testnet_oro/join_oro.sh)
* [Join Testnet Oro CV](https://raw.githubusercontent.com/KiiChain/testnets/refs/heads/main/testnet_oro/join_oro_cv.sh)
