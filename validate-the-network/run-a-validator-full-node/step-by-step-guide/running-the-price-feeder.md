---
description: How to run your own Oracle and price feeder
hidden: true
---

# Running the Price feeder

The Price Feeder is an essential component for validators added to Kiichain since version v4.0.0 to provide accurate cryptocurrency price data to the Kiichain network using the [Oracle module](../../getting-started/what-is-an-oracle.md). Follow these steps to set it up:

**Prerequisites**

* A running Kiichain validator node
* At least `100000000ukii` in your validator account for feeder delegation

### **Installation Steps**

1. **Download the Setup Script**

```
wget https://raw.githubusercontent.com/KiiChain/testnets/main/testnet_oro/run_price_feeder.sh
chmod +x run_price_feeder.sh
```

2. **Edit Configuration Variables**

Open the script and modify these values at the top:

```
VALIDATOR_ACCOUNT_NAME="your_validator_account_name"  # Your validator key name
VALIDATOR_ADDRESS="kiivaloper1..."                   # Your validator operator address
KEYRING_PASSWORD="your_password"                     # Keyring password
KEYRING_BACKEND="os"                                 # use your preference
```

3. **Run the Installation**

```
./run_price_feeder.sh
```

The script will automatically:

* Build and install the price-feeder
* Create a dedicated feeder account
* Delegate price reporting rights
* Fund the feeder account
* Configure the systemd service

4. **Verify Operation**

Check the service logs:

```
journalctl -fu price_feeder.service -n 100
```

Look for the following log with the success voting and broadcast process, should look as this example.

```
INF Going to broadcast vote exchange_rates=627.294973247184155604ubnb,
87373.053355393894624692ubtc,2026.187799244052648861ueth,
138.957568367835068788usol,0.999880568783958689uusdc
```

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
If you are using **os**  as `KEYRING_BACKEND` make sure you have set the env variable `PRICE_FEEDER_PASS` with your **keyring password.** If no&#x74;**,** the script run\_price\_feeder.sh will ask you to type your keyring password using the CLI.
{% endhint %}

### Current exchange rates fetched by the price feeder and handled by the Oracle module

These are the prices stored on the blockchain (represented in USD).

* $BTC
* $ETC
* $SOL
* $XRP
* $BNB
* $USDT
* $USDC

## References

* [Oracle definition by Kii team](../../getting-started/what-is-an-oracle.md)
* [Oracle definition by Cosmos](https://docs.cosmos.network/v0.50/tutorials/vote-extensions/oracle/what-is-an-oracle)
* [Run the price feeder](https://github.com/KiiChain/testnets/blob/main/testnet_oro/run_price_feeder.sh)
* [Price feeder README](https://github.com/KiiChain/kiichain/blob/main/oracle/price_feeder/README.md)
* [Oracle endpoints](../../../build-on-kiichain/endpoints-cosmos-1/kiichain/oracle.md)

