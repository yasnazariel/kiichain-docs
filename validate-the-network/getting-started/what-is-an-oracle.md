---
description: >-
  An oracle is a blockchain component that provides external real-world data and
  store on the Blockchain
hidden: true
---

# What is an Oracle?

### What is the Kii Oracle? <a href="#what-is-a-cosmos-validator" id="what-is-a-cosmos-validator"></a>

The **Kii Oracle** is a decentralized price feed system that provides secure and reliable real-world market data (primarily cryptocurrency prices and tokenized assets) to the KiiChain blockchain. Unlike simple data oracles, it implements a robust **validator-based consensus mechanism** where:

* **Trusted validators** independently fetch prices from multiple exchanges
* Submitted prices are aggregated using a **weighted median** (where voting power corresponds to a validator's stake)
* Votes that deviate beyond predefined **standard deviation thresholds** are automatically rejected, preventing price manipulation
* The final agreed-upon price is recorded on-chain through on-chain **Oracle** module

This dual-layer system (off-chain data collection + on-chain consensus) ensures DeFi applications like stablecoins and lending protocols receive **tamper-resistant price data** while maintaining full decentralization.

### What kind of information does the Kii Oracle store? <a href="#what-is-a-cosmos-validator" id="what-is-a-cosmos-validator"></a>

The Kii Oracle stores and manages:

* **Cryptocurrency price pairs** (e.g., `BTC/USDT`, `ETH/USDT`) with:
  * **Chain-denominated values** (e.g., `ubtc`, `uusdt` for KiiChain assets).
  * **Deviation thresholds** to prevent volatile or manipulated data.
  * **Provider lists** (e.g., Binance, Coinbase) for data aggregation.
* **Validator-submitted prices**, aggregated into a consensus value.

The data is stored on-chain in the Oracle module’s state and updated periodically by the `price-feeder` to ensure accuracy.

### **What is the Purpose of an Oracle in Kiichain**?

An Oracle in **Kiichain** serves as the **essential bridge** between blockchain-based financial applications and real-world market data. It provides **secure, decentralized, and tamper-proof price feeds** that enable smart contracts to interact with external economic information and empowers developers to build financial tools with key requirements such as **open, fair, and resilient**.
