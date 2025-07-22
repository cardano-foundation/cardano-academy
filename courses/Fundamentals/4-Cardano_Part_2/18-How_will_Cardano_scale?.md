Scalability is a blockchain’s ability to handle usage or adoption. Measuring scalability is not simply measuring the TPS (transactions per second), it is more nuanced than that. TPS is perhaps the crudest metric to use as transactions occur in a variety of sizes and formats. Instead, we must consider a wide range of metrics: 

- Throughput is the quantity of data that a system can process in a given length of time. 
- Script execution time, how long was the CPU busy for? 
- Finality is the amount of time it takes for a transaction to become immutable
- Concurrency is the amount of work various actors can do without interfering with one another.
- The actual size of transaction(s) 

Any blockchain can appear fast using tiny transaction sizes and no scripts. Some high profile blockchains have centralized characteristics such as a minority of validators controlling disproportionate amounts of stake. It’s easy for a blockchain to compromise on decentralization then boast astronomical TPS figures. 

We should also note that throughput means something different in a UTXO system than it does in an account-based system. TPS on Cardano is yet more nuanced due to its native asset capability. eUTXO allows hundreds, even thousands, of native assets to be transferred in a single transaction. Nearly everything on Cardano occurs as a transaction, and generally speaking resources are consumed from these types of activities…transferring ada, issuing assets, executing smart contracts, voting and adding metadata. A more accurate metric is therefore TPT (transactions per transaction). To understand and visualize how transactions work on Cardano, visit eUTtxO.org, a blockchain explorer which presents a live view of blocks, and their contents, being created. 

There is no ‘magic bullet’ for scaling blockchains, it’s done by tweaking parameters and combining different solutions that generally fall into two categories:

- Layer 1 solutions: upgrades applied to the mainchain, ie. Cardano. 
- Layer 2 solutions: offloading workloads, extending functionality and integrating other blockchains with sidechains, ZK rollups and state channels.

Scaling solutions are usually categorized as either On-chain solutions which encompass block size increases, pipelining, input endorsers, parameter adjustments, Plutus script enhancements, node enhancements and on-disk storage improvements. Then there are Off-chain solutions including sidechains, partner chains, Hydra, off-chain computing and Mithril. We’ll dive deeper into these solutions in future courses. 

There's also the actual size of the blockchain to take into account. Blockchains can store data infinitely. All transactions recorded on the blockchain are logged regardless of relevance as the number of transactions per second increases. A bloated blockchain leads to slower sync times for wallets, it’s like flooding your basement with water. It’s likely to make life difficult in the long term. Cardano’s architecture focuses on moving a lot of the computation off chain and storing the minimum on the mainchain. Bitcoin’s blockchain size passed half a terabyte in late 2023, Ethereum, on the other hand, requires wallets to download over a terabyte of data to sync. Cardano compares favorably at 177 GB if you consider Solana has bloated to 3.8 terabytes.
