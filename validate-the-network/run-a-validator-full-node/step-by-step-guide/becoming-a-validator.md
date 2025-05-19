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

To create a validator, first you will need to create a JSON with your validator information.

This template can be used when creating the validator:

```json
{
    "pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"C2xVqc+u101PQShdTJxGOF2HFCtYWwMDYLl4r2swiGE="},
    "amount": "1000000000000000000000akii",
    "moniker": "MY VALIDATOR",
    "identity": "optional identity signature (ex. UPort or Keybase)",
    "website": "validator's (optional) website",
    "security": "validator's (optional) security contact email",
    "details": "validator's (optional) details",
    "commission-rate": "0.1",
    "commission-max-rate": "0.2",
    "commission-max-change-rate": "0.01",
    "min-self-delegation": "1"
}
```

Where:

* `pubkey` : Validator's public key used for signing blocks (ed25519).&#x20;
* `amount`: Amount of tokens to self-delegate (e.g., 1000 akii with 18 decimals).
* `moniker`: Validator's display name.
* `identity` (optional): Identity string (e.g., Keybase or UPort for verification).
* `website` (optional): Validator’s website URL.
* `security` (optional): Security contact email for incident disclosure.
* `details` (optional): Additional description of the validator.
* **`commission-rate`** :Initial commission rate (e.g., 0.1 = 10%).
* **`commission-max-rate`**: Maximum commission rate allowed (e.g., 20%).
* **`commission-max-change-rate`**: Max daily change in commission (e.g., 1%).
* `min-self-delegation`: Minimum tokens validator must always self-delegate to stay active.

To apply, you can use the following command:

```bash
# Basic chain information
CHAIN_ID="oro_1336-1"
VALIDATOR_KEY_NAME=<my-validator-key>

# Apply the create validator transaction
kiichaind tx staking create-validator /
  ./validator.json /
  --chain-id=$CHAIN_ID /
  --gas="auto" /
  --gas-adjustment 1.3 /
  --gas-prices="1000000000akii" /
  --from=$VALIDATOR_KEY_NAME
```

{% hint style="warning" %}
The transaction must be done on the machine running the node

* An additional flag `--node` can be passed to point to an available RPC node
{% endhint %}

Further instructions on how to run a validator can be found at [Running a Validator](https://hub.cosmos.network/main/validators/validator-setup.html).
