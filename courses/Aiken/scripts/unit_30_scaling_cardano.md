# Scaling Cardano

To recap, we discussed how account-based ledgers are simple and intuitive. But, as the state of an account is global, they have trouble scaling. So all transactions interacting with an account impact this one state. This, along with sequencing requirements, can drastically slow down throughput. Scaling a blockchain means improving its design using various techniques and solutions. Many of them are complementary and interdependent on each other.

The overall goal is to increase throughput. Note that in a distributed system like a blockchain, transactions are only eventually valid. 

Cardano’s Ouroboros consensus mechanism is similar to Nakamoto-style consensus, with probabilistic finality of blocks.

The assurance that a block’s transactions will endure on-chain improves with the addition of new blocks, commonly referred to as the number of confirmations. The longer a transaction has been in a node’s mempool, the more approvals it will have and so would usually have higher priority when added to a block. Cardano transactions operate on a first-in, first-out basis.

Before we go any further, we should clarify a few terms that are sometimes used interchangeably. 

- **Throughput** is the quantity of data that a system can process in a given length of time. 
- We’ll see later the **execution cost** is quantified in terms of the number of steps the virtual machine needs to complete a task, as well as the quantity of memory it requires.
- **Latency** is the time it takes a transaction to appear in a block appended to the blockchain. 
- **Finality** is the amount of time it takes for a transaction to become immutable and final for everyone in the system.
- **Concurrency** is the amount of work that various actors can do without interfering with one another.

At time of writing, blocks on the Cardano mainnet are created approximately every 20 seconds, with a max block size of 90kB and max transaction size of 16kB. You can review all the latest parameter settings on cexplorer. 

Cardano’s arsenal of scalability solutions build upon the deterministic behavior and elegance of the eUTxO model.

## Questions

1. What is the primary goal of scaling a blockchain?

**A. To increase throughput**
B. To reduce energy consumption
C. To enhance decentralization
D. To improve security

2. What is throughput in the context of blockchain?

A. The amount of time it takes for a transaction to be confirmed
B. The number of transactions that can be stored in a block
**C. The quantity of data that can be processed in a given time**
D. The speed at which blocks are added to the blockchain

3. What is latency in the context of blockchain?

A. The amount of time it takes for a transaction to become final
B. The delay in propagating blocks across the network
**C. The time it takes for a transaction to appear in a block**
D. The variability in transaction confirmation times

4. What is finality in the context of blockchain?

A. The average number of confirmations for a transaction
B. The guarantee that a transaction will not be reversed
**C. The time it takes for a transaction to become immutable**
D. The total number of transactions processed by the blockchain

5. What is concurrency in the context of blockchain?

A. The ability of the blockchain to handle multiple transactions simultaneously
B. The degree to which different parts of the blockchain can operate independently
**C. The amount of work that can be done without interference**
D. The level of agreement among nodes on the state of the blockchain


