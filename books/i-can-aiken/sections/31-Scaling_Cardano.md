**Scaling Cardano** 

To recap, we discussed how account-based ledgers are simple and intuitive. But, as the state of an account is global, they have trouble scaling. So all transactions interacting with an account impact this one state. This, along with sequencing requirements, can drastically slow down throughput. Scaling a blockchain means improving its design using various techniques and solutions. Many of them are complementary and interdependent on each other.

The overall goal is to increase throughput. Note that in a distributed system like a blockchain, transactions are only eventually valid. Cardano’s Ouroboros consensus mechanism is similar to Nakamoto-style consensus, with probabilistic finality of blocks. For the diagram below, our goal is to have a fat, short pipe symbolizing high throughput and short settlement time.

**Figure 34**: Throughput and settlement 

The assurance that a block’s transactions will endure on-chain improves with the addition of new blocks, commonly referred to as the number of confirmations. The longer a transaction has been in a node’s mempool, the more approvals it will have and so would usually have higher priority when added to a block. Cardano transactions operate on a first-in, first-out basis. 

**Figure 35**: Cardano state transition

Before we go any further, we should clarify a few terms that are sometimes used interchangeably. 
- **Throughput** is the quantity of data that a system can process in a given length of time. 
- We’ll see later the **execution cost** is quantified in terms of the number of steps the virtual machine needs to complete a task, as well as the quantity of memory it requires.
- **Latency** is the time it takes a transaction to appear in a block appended to the blockchain. 
- **Finality** is the amount of time it takes for a transaction to become immutable and final for everyone in the system.
- **Concurrency** is the amount of work that various actors can do without interfering with one another. 

At time of writing, blocks on the Cardano mainnet are created approximately every 20 seconds, with a max block size of 90kB and max transaction size of 16kB. You can review all the latest parameter settings on cexplorer.[^1]: Cardano’s arsenal of scalability solutions build upon the deterministic behavior and elegance of the eUTxO model.  

[^1]: Cardano parameters, cexplorer.io/params
