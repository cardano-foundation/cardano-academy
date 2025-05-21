Sharding is a term that should be familiar to anyone from the Web2 database world. It involves slicing a database into smaller pieces, or shards. The result is the database is 'more than the sum of its parts.' The aggregate performance of the shards is greater than before.

Sharding is a form of parallelism in a system where each shard operates independently and can process its own set of transactions. If this parallel execution of transactions increases the overall blockchain efficiency and throughput, it is a big win for scalability. Each shard maintains its portion of the global state. Think of the global state of the entire blockchain as the aggregate of all these local states. 

What we described is a high level, simplistic view. To enable this to work in practice, cross-shard communication must take place. Transaction data needs to be exchanged between different shards. Now earlier design decisions begin to hit home, as the UTxO model is a lot more suited for sharding than the account-based model. 

**Figure 19:** UTxO sharding

Remember earlier we said the **transaction** serves as the fundamental unit of validation for **UTxO**. Cardano’s transaction validations are predictable, or deterministic. Multiple nodes can validate transactions in parallel and, crucially, in any order, regardless of the block.  

In the Ethereum **account-based** model, the **block** is the primary unit of validation. Transactions depend on each other and cannot be validated in isolation. They must always factor in the prevailing global state. Think of Ethereum’s global state as a long sequence of transactions. The outcome of your transaction validation depends on your position in the sequence.

For UTxO-based blockchains, implementing sharding is relatively easy. The UTxO set facilitates parallelism and validation of transactions independently within each shard. Validation happens regardless of the block and the transaction’s position in the block. Most of this aggregation of transaction outputs can take place off chain, reducing the load on-chain. 

The difference is not trivial if we are trying to implement sharding for a ‘world computer.’ Imagine you are buying ice cream on a warm day, and there is a long queue for the van. Would you rather exchange a voucher for an agreed price or be at the mercy of the account-based system in which the price of the ice cream can vary, depending on the appetite for ice cream globally at the time?
