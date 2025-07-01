---
description: How to run your own Oracle and price feeder
---

# Running the Price feeder

[The Price Feeder](https://github.com/KiiChain/price-feeder) is an application used by validators to easily provide price feeds to the oracle module. The application abstracts away all the Oracle module requirements to the validators.

{% hint style="warning" %}
Only validators are required to run the price-feeder. The module doesn't affect full nodes.

* Validators who don't provide feeds for the oracle module **will be slashed.**
{% endhint %}

## Price feeder details

[The Price Feeder](https://github.com/KiiChain/price-feeder) is an essential component for validators added to Kiichain since version **v3.0.0** to provide accurate cryptocurrency price data to the Kiichain network using the [Oracle module](../getting-started/what-is-an-oracle.md).&#x20;

### Prerequisites

* A running Kiichain validator node
* At least `1000000000000000000akii` (1 Kii) in your validator account for feeder delegation

There are **no fees to run the price feeder**:

* As long as it's voting once per voting period
* And the voter is the expected address for each validator

### Exchange Rates and Providers

These are the prices stored on the blockchain (represented in USD).

* $BTC
* $ETC
* $SOL
* $XRP
* $BNB
* $USDT
* $USDC
* $TRX

These are the providers by default on the price feeder:

* [Binance](https://www.binance.com/en)
* [MEXC](https://www.mexc.com/)
* [Coinbase](https://www.coinbase.com/)
* [Gate](https://www.gate.io/)
* [Huobi](https://www.huobi.com/en-us/)
* [Kraken](https://www.kraken.com/en-us/)
* [Okx](https://www.okx.com/)

### Feeder account

One important concept about the Oracle module and price-feeder is the feeder account.

The feeder is an account that:

* Separates your validator address from the account handling oracle feeds
  * This increases the security of your validator's main address
  * Keeps the validator’s signing key offline

{% hint style="warning" %}
We highly recommend using a feeder account for the price-feeder:

* Make sure that the feeder or any other accounts used on the price-feeder will not be used anywhere else:
  * Changes in account sequence may make the price-feeder fail to send TXs
{% endhint %}

#### Feeder account setup

To set up or update your feeder account, you can use the following TX:

```bash
# Set the variables for the transaction
FEEDER_ADDR=kii1... # Update with your feeder address
# The key name of the signer
# Should be the same as the one used to manage your validator
FROM_KEY_NAME=<key_name>

# Create the feeder
kiichaind tx oracle set-feeder $FEEDER_ADDR \
    --from $FROM_KEY_NAME --keyring-backend test \
    --gas auto --gas-adjustment 1.5 --gas-prices 100000000000akii \
    --node https://rpc.uno.sentry.testnet.v3.kiivalidator.com --chain-id oro_1336-1
    
# Fund feeder account
kiichaind tx bank send <validator-wallet> $FEEDER_ADDR 1000000000000000000akii \
    --from $FROM_KEY_NAME --keyring-backend test \
    --gas auto --gas-adjustment 1.5 --gas-prices 100000000000akii \
    --node https://rpc.uno.sentry.testnet.v3.kiivalidator.com --chain-id oro_1336-1
```

Upon TX success, the `FEEDER_ADDR` can then be used to provide price feeds for the Oracle module.

{% hint style="warning" %}
Make sure that the feeder address has some Kii in its balance:

* Although providing feeds is free, the account must exist on the chain and have a balance available
{% endhint %}

## **Installation Steps**

The price feeder can be easily installed with our bootstrap script:

* [Run price feeder](https://raw.githubusercontent.com/KiiChain/testnets/main/testnet_oro/run_price_feeder.sh)

The script will automatically:

* Build and install the price-feeder
* Create a dedicated feeder account
* Delegate price reporting rights
* Fund the feeder account
* Configure the systemd service

{% hint style="success" %}
We highly recommend using this bootstrap script to setup the price-feeder.

You can also use it as a reference when preparing your own deployment.
{% endhint %}

### Manual installation

You can also install the price-feeder manually by following these steps:

1. **Build and install the price feeder**

```bash
# Clone the price feeder
git clone git@github.com:KiiChain/price-feeder.git

# Install the application
cd price-feeder
make install

# Test if the binary was installed correctly
price-feeder version
```

#### 2. Configure the price-feeder

Download our example config with:

```bash
wget https://raw.githubusercontent.com/KiiChain/price-feeder/refs/heads/main/config.example.toml
mv config.example.toml price-feeder.config
```

Now read the file and update all the main configurations based on our next section:

* [Price feeder configuration](running-the-price-feeder.md#price-feeder-configuration)

3. **Test your configuration**

You can always test your configuration using:

```bash
# Export your feeder private key
export PRICE_FEEDER_PASS=<my_keyring_pass>

# Run the price feeder
# You may also provide the argument --skip-password if your keyring is test
# or has no password
price-feeder start price-feeder.config
```

* Pay attention to the logs and errors
* After running for a few seconds, all errors should clear out
* If errors persist, your feeder address may be configured incorrectly

4. **Create the systemctl service**

Upon confirmation that the price feeder is correctly configured, you can turn it into a service with this example systemd service file:

```bash
[Unit]
Description=Price Feeder
After=network-online.target
 
[Service]
User=root
Type=simple
Environment="PRICE_FEEDER_PASS=YOUR_KEYRING_PASSWORD"
ExecStart=/usr/bin/price-feeder start /price_feeder_config.toml
Restart=on-failure
RestartSec=3
LimitNOFILE=6553500
 
[Install]
WantedBy=multi-user.target
```

Don't forget to check:

* Your user is not `root`
* The path for the price-feeder and the path for the configuration file
* Your keyring password

5. **Verify Operation**

Check the service logs:

```bash
journalctl -fu price_feeder.service
```

#### Price feeder configuration

There are multiple configurations that are important when managing the price feeder:

* The main template for configuration [can be found here](https://github.com/KiiChain/price-feeder/blob/main/config.toml)

Some important configurations are:

```toml
[account]
# The account name to use for signing transactions
# Can be the validator master account or a feeder account
address = "kii1..."
# The validator who is voting
validator = "kiivaloper1..."
# The prefix for the keys
prefix = "kii"
# The chain ID for signatures
chain_id = "oro_1336-1"
```

Here you should set up the details of your account:

* `address`: This is the feeder address used on the price-feeder
* `validator`: This is your validator address. This is important when sending the feeds to the Oracle module

```toml
[rpc]
# The RPC endpoint for the node that will send transactions
grpc_endpoint = "localhost:9090"
# The timeout for RPC calls
rpc_timeout = "500ms"
# The Tendermint RPC endpoint for querying the blockchain
tmrpc_endpoint = "http://localhost:26657"
```

The above defines your RPC configuration:

* **It's highly recommended to point the endpoints to local nodes**, but pointing to remote nodes is also possible

```toml
[keyring]
# The keyring backend to use for storing keys
backend = "os"
# The keyring directory where keys are stored
dir = "~/.kiichain"
```

This defines your keyring configuration:

* We highly recommend using OS as your keyring for the feeder key
* The Keyring password should be provided with the environment key `PRICE_FEEDER_PASS`



#### **Important Note: Oracle Voting Performance Requirements**

Validators running the **Price Feeder** must maintain a high success rate when submitting price votes. The Oracle module enforces this through a **slashing mechanism**:

* **`MinValidPerWindow` Parameter**:\
  This governance-defined threshold (5%) sets the **minimum percentage of successful votes** a validator must submit per voting window (3600 blocks).
* **Penalty for Underperformance**:\
  If a validator’s ratio of **successful votes / total votes** falls below `MinValidPerWindow`:
  * The validator is **automatically jailed**
  * It cannot participate in consensus or earn staking rewards
  * Manual unjailing requires a governance proposal or fixed downtime duration
* **Recommendations for Validators**:
  * Monitor your feeder’s logs (`journalctl -fu price_feeder.service`)
  * Ensure stable API connections to price providers
  * Maintain sufficient gas fees for timely transactions

{% hint style="warning" %}
If you are using **os** as `KEYRING_BACKEND` make sure you have set the env variable `PRICE_FEEDER_PASS` with your **keyring password.** If no&#x74;**,** the script run\_price\_feeder.sh will ask you to type your keyring password using the CLI.
{% endhint %}

## References

* [Oracle definition by Kii team](../getting-started/what-is-an-oracle.md)
* [Oracle definition by Cosmos](https://docs.cosmos.network/v0.50/tutorials/vote-extensions/oracle/what-is-an-oracle)
* [Run the price feeder](https://github.com/KiiChain/testnets/blob/main/testnet_oro/run_price_feeder.sh)
* [Price feeder README](https://github.com/KiiChain/price-feeder/blob/main/README.md)
* [Oracle module details](../../build-on-kiichain/modules/oracle.md)

## Acknowledgment

This is the Kiichain version of the incredible work of SEI on the price feeder module. The original implementation is available at [SEI's price-feeder](https://github.com/sei-protocol/sei-chain/tree/main/oracle/price-feeder).
