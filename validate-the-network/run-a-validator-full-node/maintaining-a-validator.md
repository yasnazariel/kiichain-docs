---
description: How to update and maintain a validator on the Kii network
---

# Maintaining a validator

This will guide you through basic operations on how to maintain a validator.

## What is a validator?

Validators are the ones responsible for committing blocks. Due to this responsibility, validators must run their own nodes and will be slashed if they become unavailable or sign blocks at the same height. Validators will also receive rewards for each block signed from fees.

## Creating a validator

1. **Key creation**

To create a validator, you first must have a key available for transactions. A new key can be created with:

```bash
kiichaind keys add $VALIDATOR_KEY_NAME
```

You will get an output such as:

```
- address: kii105xft78q4wm565sn62chq4dxxvzq6uhqu0dawp
  name: "1234"
  pubkey: '{"@type":"/cosmos.evm.crypto.v1.ethsecp256k1.PubKey","key":"AxA37KswOGRQJ7R4JsDMbglhqh0TcPoiPEq/GCNZ1AJx"}'
  type: local


**Important** write this mnemonic phrase in a safe place.
It is the only way to recover your account if you ever forget your password.

mom half sting horn fashion pizza citizen lonely random february knee miss vibrant peasant among pool suffer street alert eager notable net leave wrestle
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

## Edit validator description

At any moment, you can update your validator public description. This description is public and is what will be shown on block explorers.

To update your delegator information you can use:

```bash
kiichaind tx staking edit-validator
  --moniker="Any moniker" \
  --website="https://kii.network" \
  --identity=6A0D65E29A4CBC8E \
  --details="Delegate on my awesome kii validator!" \
  --chain-id=<chain_id> \
  --gas="auto" \
  --gas-adjustment 1.3 \
  --gas-prices="1000000000akii" \
  --from=<key_name> \
  --commission-rate="0.10"
```

Where:

* `--from`  must be the operator of the validator
* `--identity` can be used as to verify identity with systems like Keybase or UPort
* `--commission-rate`must follow these rules:
  * Must be between 0 and the validator's `commission-max-rate`
  * Must not exceed the validator's `commission-max-change-rate` which is maximum % point change rate **per day**.

{% hint style="danger" %}
Neither `commission-max-rate` and `commission-max-change-rate` can be changed after validator creation.
{% endhint %}

## Unjail Validator

Your validator may get jailed for downtime. To unjail your validator you must use the following transaction:

```
kiichaind tx slashing unjail \
 --from=<key_name> \
 --chain-id=<chain_id>
 --gas="auto" \
 --gas-prices="1000000000akii"
```

## Halting Your Validator <a href="#halting-your-validator" id="halting-your-validator"></a>

You may want to halt your validator for maintenance or a coordinated upgrade. You can gracefully halt your validator by setting it `halt-height`to the height you want to pause your validator. The node will shutdown with a zero exit code at that given height after committing the block.
