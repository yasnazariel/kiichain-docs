---
description: How to run your own Kiichain Validator
---

# Becoming a Validator

The configuration followed before, set your node as a **full node**, this page will guide you to upgrade your node into a validator. &#x20;

## Becoming a validator

Validators are mainly responsible&#x20;

* **The build must be done on top of the upgrade tag (E.g. v1.0.1, v2.0.0)**
* Check the section [Binary Installation](becoming-a-validator.md#binary-installation) on how to do it

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

&#x20;validating and committing blocks. The main advantages of becoming a validator are:

* **Fees.** Each transaction has fees, and validators are the main entry points of fee distribution. And due to his help on decentralization, part of the fee is exclusive for validators.

## Creating a validator

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

To create a validator, you can use the following command:

```bash
# Basic chain information
CHAIN_ID="oro_1336-1"

# Define the validator information
MONIKER=<my-moniker>
AMOUNT=1000000000000000000000akii # 1000 kii as self delegation
COMMISSION_MAX_CHANGE_RATE=0.1
COMMISSION_MAX_RATE=0.1
COMMISSION_RATE=0.1
MIN_SELF_DELEGATION_AMOUNT=1000000000000000000

kiichaind tx staking create-validator \
  --amount=$AMOUNT \
  --pubkey=$(kiichaind tendermint show-validator) \
  --moniker=$MONIKER \
  --chain-id=$CHAIN_ID \
  --commission-rate=$COMMISSION_RATE \
  --commission-max-rate=$COMMISSION_MAX_RATE \
  --commission-max-change-rate=$COMMISSION_MAX_CHANGE_RATE \
  --min-self-delegation=$MIN_SELF_DELEGATION_AMOUNT \
  --gas="auto" \
  --gas-adjustment 1.3 \
  --gas-prices="1000000000akii" \
  --from=$VALIDATOR_KEY_NAME
```

{% hint style="warning" %}
The transaction must be done on the machine running the node

* An additional flag `--node` can be passed to point to an available RPC node
{% endhint %}

Further instructions on how to run a validator can be found at [Running a Validator](https://hub.cosmos.network/main/validators/validator-setup.html).
