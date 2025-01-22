---
description: Calculate rewards at the beginning of each epoch.
---

# Block Rewards Formula

Block rewards are distributed proportionally to all validators relative to their voting power. This means that even though each validator gains KII with each reward, all validators maintain equal weight over time.

For example, 10 validators have equal voting power and a commission rate of 1%. For this example, the reward for a block is 1000 KII and each validator has 20% of self-bonded KII. These tokens do not go directly to the proposer. Instead, the tokens are evenly spread among validators. So now each validator's pool has 100 KII. These 100 KII are distributed according to each participant's stake:

* Commission:  `100*80%*1% = 0.8 KII`
* Validator gets: `100\*20% + Commission = 20.8 KII`
* All delegators get: `100\*80% - Commission = 79.2 KII`

Then, each delegator can claim their part of the 79.2 KII in proportion to their stake in the validator's staking pool.
