---
description: Staking rewards and validator commissions.
---

# Incentive to stake

### Revenue

Validators and delegators earn revenue in exchange for their services. This revenue is given in two forms:

1. **Block provisions (KIIs)**: They are paid in newly created KIIs. Block provisions exist to incentivize KII holders to validate and stake the network.&#x20;
2. **Transaction fees (KIIs)**: Each transfer on Kiichain comes with transaction fees. These fees can be paid in any currency that is whitelisted by the Hub's governance. Fees are distributed to bonded KII holders in proportion to their stake.&#x20;

Each validator receives revenue based on their total stake. Before this revenue is distributed to delegators, the validator can apply a commission. In other words, delegators have to pay a commission to their validators on the revenue they earn. Let us look at a concrete example:

We consider a validator whose stake (i.e. self-delegated stake + delegated stake) is 10% of the total stake of all validators. This validator has 20% self-delegated stake and applies a commission of 10%. Now let us consider a block with the following revenue.

### Validator Commission

We can see the validator commission with the following example:

* 990 KIIs will be rewarded in block provisions
* 10 KIIs will be rewarded in transaction fees
* This amounts to a total of 1000 KIIs in rewards

Our validator's staking pool represents 10% of the total stake, which means the pool obtains 100 KIIs. Now let us look at the internal distribution of revenue:

* Commission = 10% \* 80% \* 100 KIIs = 8 KIIs
* Validator's revenue = 20% \* 100 KIIs + Commission = 28 KIIs
* Delegators' total revenue = 80% \* 100 KIIs - Commission = 72 KIIs

Then, each delegator in the staking pool can claim their portion of the delegators' total revenue.
