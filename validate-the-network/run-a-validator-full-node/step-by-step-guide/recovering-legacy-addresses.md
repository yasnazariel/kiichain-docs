---
description: Legacy addresses can be recovered
---

# Recovering Legacy Addresses

With the upcoming Kiichain upgrade, wallet key handling is changing to support Ethereum-compatible tooling and address formats. This guide explains what's changing and how to recover your old wallets safely.

## What’s Changing?

#### **1. New Key Type**

* Old Type: `secp256k1`&#x20;
* New Type: `eth_secp256k1`&#x20;

> This enables Ethereum-compatible signatures (e.g., MetaMask, Keplr EVM support).

**2. New Coin Type**

* Old Coin Type: `118` (standard Cosmos)
* New Coin Type: `60` (Ethereum standard)

> This changes the way addresses are derived from your mnemonic.

## Recovering Existing Wallets

To recover old wallets (e.g., validator rewards wallets or delegator accounts) that were created before the upgrade:

```bash
kiichaind keys add <key_name> \
  --keyring-backend test \
  --recover \
  --coin-type 118 \
  --key-type secp256k1
```

* Replace `<key_name>` with your desired key name.
* Input your existing **mnemonic** when prompted.

## Need to Check What Type a Key Was Created With?

Unfortunately, `kiichaind keys list` **does not show the coin type**. You’ll need to recall which mnemonic was created with which derivation path. To avoid confusion:

* Use **clear key names** like `validator_old`, `wallet_eth`.
* Document the **coin type** and **key type** when generating keys.
