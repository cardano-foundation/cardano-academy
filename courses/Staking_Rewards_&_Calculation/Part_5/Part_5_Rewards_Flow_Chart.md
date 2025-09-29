The process begins with the calculation of new reserves, fees, the total rewards pot, and the treasury. Subsequently, pool rewards are determined based on this total rewards pot. The pool rewards are used to calculate the stake pool delegators’ and stake pool operators’ rewards. Due to the requirement for snapshot-based calculations, it can happen that a stake account might become unregistered after taking a snapshot. Consequently, the stake account cannot receive rewards after the calculation is completed, necessitating custom rules to handle those special situations. 

These rules are naturally spread across the code base, as the calculation process itself is distributed over time. The cardano-ledger repository aggregates most of the business logic, alongside relevant documentation. You can find some additional components required for this process in the cardano-node itself or in the ouroboros-network repository.  

Remember, a slot is every second on Cardano… and the code gets executed using a slot-based scheduler. This scheduling method can prove challenging to read and follow for those unfamiliar with the codebase. While developers have introduced certain optimizations to enhance the calculation's performance, these optimizations can make the code less straightforward to understand. The open source rewards calculation aims to address these challenges while maintaining the robust features native to the Cardano network.  

Cardano ledger specification includes multiple equations that collectively define the flow of ada at the end of each epoch. Each node independently calculates the rewards per epoch in a distributed manner, with any potential rewards then distributed based on the consensus mechanism. Notably, no one entity completes this calculation, and no one can withhold rewards. These ada rewards, calculated every epoch, derive from the interaction of two sources: transaction fees and monetary expansion.

- Transaction fees: At the end of each epoch the value from the fee pot–the sum of all transaction fees in that epoch–goes into the total rewards pot.
- Monetary expansion: In addition to transaction fees, a fixed percentage of the reserve goes into the same total rewards pot.  

The total rewards pot is then divided into two segments. The first part goes into the treasury, while the second forms the stake pool rewards pot. Notably, the reserves originally started with approximately 14 billion ada and have decreased gradually.  

Simultaneously, another calculation computes the pool reward, utilizing the stake pool parameters that with the apparent pool performance determine the individual stake pool rewards. The resulting value forms the foundation for calculating both delegator and operator rewards. Importantly, all these calculations depend on protocol parameters. The rewards calculation forms an integral part of the Cardano blockchain ecosystem, making it crucial to educate people on how it works.  

This knowledge empowers people to choose a stake pool that fits with their vision and values.   

Note that Cardano uses a Chimeric Ledger, where reward accounts are distinct from UTXOs, and are more akin to accounts in account-based blockchains. They are used for accumulating staking rewards, rather than using UTXOs, in order to avoid creating a large number of UTXOs with tiny values. Reward accounts are special on Cardano and cannot be created arbitrarily. When a user registers a staking credential, the system automatically creates a reward account.
