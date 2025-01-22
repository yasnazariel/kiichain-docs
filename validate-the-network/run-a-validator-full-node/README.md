---
description: Initial steps before announcing your entry as a validator
---

# Run a Validator / Full Node

**Introduction**&#x20;

Kiichain is a cosmos based blockchain that relies on a set of validators that are responsible for committing new blocks in the blockchain. These validators participate in the consensus protocol by broadcasting votes that contain cryptographic signatures signed by each validator's private key.

Validator candidates can bond their own KII and have KII "delegated", or staked, to them by token holders. Kiichain has an open set of 100 validators who reviews rewards, but over time the number of validators can be increased with governance proposals. The validators are determined by the total number of KII tokens delegated to them — the top 100 validator candidates with the most voting power are the current Kii validators.

Validators and their delegators earn KII as block provisions and tokens as transaction fees through execution of the Tendermint consensus protocol. Note that validators can set a commission percentage on the fees their delegators receive as additional incentive.

If validators double sign or are offline for an extended period, their staked KII (including KII of users that delegated to them) can be slashed. The penalty depends on the severity of the violation.

**Hardware**&#x20;

For validator key management, validators must set up a physical operation that is secured with restricted access. A good starting place, for example, would be co-locating in secure data centers.

Validators are expected to equip their datacenter location with redundant power, connectivity, and storage backups. Expect to have several redundant networking boxes for fiber, firewall, and switching and then small servers with redundant hard drive and failover.

As the network grows, bandwidth, CPU, and memory requirements rise. Large hard drives are recommended for storing years of blockchain history, as well as significant RAM to process the increasing amount of transactions.

**Create a Validator Website**&#x20;

To get started as a validator, create your dedicated validator website and signal your intention to become a validator in the Kii Discord validator channel. Posting your validator website is essential because delegators want to have information about the entity who is receiving their delegated KII.

**Seek Legal and Tax Advice**&#x20;

As always, do your own research and seek legal advice if you intend to run a validator node.

**Community**&#x20;

Discuss the finer details of being a validator on our community Discord. Follow Kii Global on all socials and sign up for the Kii newsletter to get regular updates.
