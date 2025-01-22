---
description: >-
  A delegator is a person or entity that wants to Stake their tokens without
  managing a node or full node.
---

# What is a delegator?

### Delegating = Staking

People who cannot or do not want to operate Validators (full nodes) can still participate in the staking process as delegators. Indeed, validators are not chosen based on their self-delegated stake but based on their total stake, which is the sum of their self-delegated stake and of the stake that is delegated to them. This is an important property, as it makes delegators a safeguard against validators who exhibit bad behavior. If a validator misbehaves, their delegators will move their KIIs away from them, thereby reducing their stake. Eventually, if a validator's stake falls under the top 100 addresses with the highest stake, they will exit the validator set.

Delegators share the revenue of their validators, but they also share the risks. In terms of revenue, validators, and delegators differ in that validators can apply a commission on the revenue that goes to their delegator before it is distributed. This commission is known to delegators beforehand and can only change according to predefined constraints (see section below). In terms of risk, delegators' KIIs can be slashed if their validator misbehaves.&#x20;

To become delegators, KII holders need to send a "Delegate transaction" where they specify how many KIIs they want to bond and to which validator. A list of validator candidates will be displayed in KII Explorer. Later, if a delegator wants to unbond part or all of their stake, they needs to send an "Unbond transaction". From there, the delegator will have to wait 21 days to retrieve their KIIs. Delegators can also send a "Rebond Transaction" to switch from one validator to another, without having to go through the 3-week waiting period.

### What is staking? <a href="#what-is-staking" id="what-is-staking"></a>

Kiichain is a public Proof-Of-Stake (PoS) blockchain, meaning that the weight of validators is determined by the amount of staking tokens (KII) bonded as collateral. These KII tokens can be self-delegated directly by the validator or delegated to the validator by other KII holders.

Any user in the system can declare their intention to become a validator by sending a `create-validator` transaction to become validator candidates.

The weight (i.e. voting power) of a validator determines whether they are an active validator.&#x20;
