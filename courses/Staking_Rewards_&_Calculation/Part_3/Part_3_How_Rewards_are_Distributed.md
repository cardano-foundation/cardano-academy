**Rewards provenance**   

In Cardano, the system doesn’t directly award transaction fees and block rewards to block producers. Instead, it collects them into a temporary reward pot. Every block made over a fixed period contributes to that pot. At the end of this period, a portion of the total rewards is sent to the Cardano treasury, a special reserve of tokens in the network used to fund its ecosystem's development. 

The remaining rewards are divided between all block producers and delegators proportionate to the blocks they minted in that period. Identification of stake pools is thus necessary, so block producers include their identifiers in the blocks they produce. 

Then, as we just saw, block producers, or simply stake pools, are assigned rewards for themselves according to their performance and chosen parameter choices. And finally, the system divides the remaining rewards proportionally among all the other delegators. So, how much reward does a block producer receive in total? Here's a brief explanation. 

The image shows that the block producer receives a portion of the total reward pot R based on a complex formula. For now, just know that the total reward R comprises two main components. First, the block includes all transaction fees of the transactions that are part of it. This component is similar to proof-of-work consensus. Second, the system calculates the monetary expansion periodically as additional rewards to be distributed to block producers for their work. 

The formula calculates the reward utilising the number of pledged tokens and the number of delegated tokens, as well as two other parameters: the Pledge Influence Factor and the Stake Pool Saturation. The consensus algorithm determines  these parameters and people commonly refer to them as a0 and k. Specifically, k refers to the ideal number of stake pools in the system, such that 1 / k represents the fraction of the maximum stake considered for a pool.

And this is why 1 / k is called the stake pool saturation: there’s no point accumulating more stake beyond that limit for a pool, as it doesn’t generate more rewards. When this happens, people say a pool is saturated, which means that delegators will likely earn fewer rewards: rewards won’t increase, but the system will split them across more delegators. This mechanism helps to prevent pools from becoming too large and puts the decentralisation and security of the system at risk.

Nevertheless, this mechanism alone isn’t sufficient. A single actor can run multiple stake pools. And this is where a0 enters the picture. As the pledge influence factor, a0 encourages stake pools to increase their pledge instead of splitting it over multiple pools by allocating more rewards to pools with high pledges. We could see that as a third incentive to limit centralization.

True to the design principles of Cardano, a0 and k are also updatable protocol parameters, so they can be adjusted to tune the system better.  

**Rewards Delay**  

As a consequence of the stake only becoming active in the following epoch it is assigned, rewards are also delayed. All the more so since rewards also depend on the pool’s performances on the epoch. And to avoid overloading the node on each epoch boundary, the system actually spreads the rewards calculation across the entire following epoch. The whole reward schedule can be a little hard to grasp, but the gist is that stake only becomes active after a delay and, thus, starts generating rewards after that delay. Then it is a cycle which repeats itself, which means that the system accrues rewards every epoch. 

To get a better understanding of how the rewards process works, visit the Cardano.org website which hosts a staking calculator for estimating your potential rewards based on the various parameters.  

**Treasury**

If you’ve been carefully following, you may have noticed we’ve only briefly mentioned the treasury when looking at the reward formula. Fundamentally, the treasury is a protocol-level tax meant to create a self-sustaining ecosystem and to fund its development. The amount cut from the total rewards is a fixed percentage, yet another protocol parameter. The system calls τ (tau), and it is currently set at 20%. 

As you can see, the treasury uses a straightforward yet highly efficient mechanism. With every epoch, it receives additional ada, which can then, in turn, be used to finance network activities or projects that benefit the overall ecosystem. Collectively deciding how to use these funds is the main focus of the Voltaire phase and a vital pillar of on-chain governance. 

Prior to the Conway era, only the genesis entities would be entitled to move funds out of the treasury, out of a quorum. These entities have periodically moved funds through Project Catalyst, an innovation fund working on a side-chain to promote innovation in the Cardano ecosystem.  

In the Conway era, the management of the treasury, amongst other governance topics, has been shifted to become a responsibility of every Ada holder, including stake pool operators. The Cardano Improvement Proposal (CIP) 1694 outlines this new design, which is a significant step towards full on-chain governance. The updated Constitution was ratified on-chain in early 2025.   
