The Cardano foundation has released an open source rewards calculation with the goal of empowering transparency and community involvement for a stronger network. Before we dive in, let's recap how staking on Cardano works… 

In proof-of-stake blockchains, as with proof-of-work, nodes compete with one another to produce blocks. However, they do not compete with hashing power. Instead, they leverage the number of blockchain tokens they control. In both proof of work and proof of stake, the chances of being selected as a block producer is like a lottery. In the former, hashing power determines the proportionality, while in the latter, the number of tokens does. The general idea is that a mechanism elects one actor in the system to produce a block at any one time.. 

Cardano's proof of stake consensus algorithm pseudo-randomly selects block producers. The distribution of tokens among all block producers forms the basis for the random function. A block producer's chances of being chosen to produce a given block increase proportionally to the number of tokens they hold compared to other block producers.. 

**Pledged, delegated and active stake**

To increase their chance of being selected, block producers, also called Stake Pool Operators, or SPOs, work towards increasing their token ownership or stake. We refer to the number of tokens a block producer personally owns and contributes to block production as their pledge.. Cardano users who do not directly participate in block production can increase a block producer's chance of being elected by delegating their stake to that block producer through their wallets. 

Fig. 2 Pledged and delegated stake

**Live stake vs Active stake** 
Live stake represents the total amount of stake that a stake pool controls. It combines the stake that is owned by the pool operator with any stake that has been delegated to the pool by other ada holders. Note that if this live stake is recorded in a snapshot, we call it the active stake. However, my live stake and active stake could be different if some of my delegators, for example, change their delegation after the system takes the snapshot. Live stake refers to the current stake at this point in time, while the system uses the active stake in the rewards calculation. SPOs are the entities that leverage the active stake for block production. The higher the SPO’s active stake, the higher the chance of being selected to create and add a new block to the blockchain.   

…An essential trait of Cardano's delegation system is that the stake remains liquid during the entire process. Said differently, there's no locking. Delegated funds can be transferred freely, and with them, their associated delegation rights. 

**Stake Distribution Snapshots**

This raises an interesting question: if the stake is fully liquid, how can we pin down the exact amount of stake used for the lottery? The answer lies in the protocol and stake distribution snapshots. 

Ouroboros divides time into 1 second slots, with blocks filled, on average, every 20 seconds. Slots are grouped into epochs lasting 5 days on mainnet currently. Many protocol mechanisms actually rely on these epochs and you’ll often hear mentions of “epoch boundaries” in the context of Cardano. This refers to the moment where the system transitions from one epoch to the next. 

From a consensus perspective, we almost always look at a snapshot of the stake distribution across an epoch and a fair question is, “a snapshot of what?” The system takes a snapshot of the stake distribution at the beginning of every epoch, reflecting the distribution from the previous epoch. However, it doesn't use this snapshot immediately because the system doesn't consider it stable yet. This delay occurs due to the probabilistic settlement of transactions in the system, which means that the system only settles information after a certain period. 

Let’s illustrate this with an example. If I delegate my stake in epoch n, the system will include it in the snapshot that occurs at the boundary between epoch n and n + 1, but it will only use it for the slot leader schedule of epoch n + 2. The system always allows at least one entire epoch for the stake to truly become active. 
