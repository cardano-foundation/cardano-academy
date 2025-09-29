**Consensus rewards and reserve**

The first kind of incentives we find in the system are consensus rewards… Ouroboros awards stake pools for their work through consensus rewards proportional to the blocks they produce. These rewards have two different sources: transaction fees and the reserve. Transaction fees are self-explanatory and correspond to the fees the system collects on all transactions in each block, per epoch. The reserve is a pot of unallocated Ada tokens the system set aside at Cardano’s genesis and hasn’t issued yet. 

Note some outliers exist, which the report details more, that are not part of the circulating supply. In every epoch, the system puts a certain percentage of the reserve into circulation through rewards. 

That percentage we call the monetary expansion and typically denote it as ρ (Rho). It is a configurable protocol parameter whose value the system currently sets at 0.3%. Thus every epoch, a maximum of 0.3% of the unallocated Ada is put in circulation, and since the reserve does not replete, this amount gradually gets smaller. At this rate, the system halves the reserve roughly every five years. 

Note that the exact amount put in circulation depends also on the blocks produced during that epoch. If the system only produces half the blocks it was expected to produce, it puts only half of the planned monetary expansion into circulation thus making the creation of new tokens entirely proportional to the actual block production. Due to the current ledger rules it could happen, that the reserve grows, if ρ (Rho) becomes very small, then that the fee pot would make the majority of the total rewards pot.

**Stake rewards and pool parameters**

On the other hand, delegators are also incentivized. In exchange for their delegation, ada holders receive a proportion of the rewards the stake pool earns according to parameters both fixed by the protocol and set by the stake pool itself.

A flat cost is taken from the total rewards granted to the pool with a minimum imposed by the protocol. This minimum is known as “min pool cost,” and it currently sits at 170 Ada. It is meant to cover the cost of running a stake pool. Then, the pool sets a variable cost–or pool margin–as a percentage. On Cardano, most pools oscillate between 1% and 3%. Once the system deducts this cost from the pool rewards, it splits the remainder across all delegates proportionally to the stake they contributed to the pool. 

Another particularly interesting parameter is called the pledge. The pledge represents a minimum amount of stake that pool owners commit to delegating to their own pool as a testimony of their seriousness and involvement. Note that pledge is optional, but think of it as a gesture by the SPO to have “skin in the game.” A high pledge means that the pool is more likely to produce blocks–and thus generate rewards–even if it hasn’t yet attracted many delegators. Pools declare the pledge when registering, and they must meet it through delegation. Should a pool not meet its declared pledge, it would receive no rewards from the system at all.  

Attracting delegation is not an exact science. Besides marketing and branding, some parameters provide a means for stake pools to compete with one another. A higher pledge or a lower variable fee is usually good to attract delegators. With incentives for stake pools, delegators, and liquid staking, Cardano ensures that a high amount of the total available stake takes part in the consensus at all times, helping secure the network against malicious actors.  
