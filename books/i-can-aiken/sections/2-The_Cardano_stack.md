Although there have been several attempts, such as the *11-layer model*,[^1] there is still no canonical standard for the blockchain stack. As most new arrivals from the Web2 world are familiar with the ubiquitous *OSI (Open Systems Interconnection) model*,[^2] it makes sense perhaps to map the Cardano blockchain stack similarly.

**Figure 1:**  Cardano blockchain stack  

**The Four Layers of the Cardano Blockchain**

1. Lying at the bottom is the **settlement layer** which hosts a financial distributed ledger derived from formal specifications. This is the foundational layer which tracks the movement of ada and native assets from one wallet to another and records transaction details.

2. Next to bottom is the **consensus layer** which is crucial for maintaining the security and robustness of the network. Here you’ll find the Ouroboros algorithm which achieves consensus on the state of the ledger. Bear in mind, the operation of any consensus mechanism is based on three key properties: safety, liveness, and finality. **Safety** is sometimes explained as 'a guarantee that nothing bad will happen'. A less vague description is that honest nodes will have the same view of the blockchain. **Liveness** is a guarantee that all validators will reach consensus on a value, so new transactions are regularly added to the blockchain. **Finality** is the point at which a blockchain transaction is widely accepted as irreversible and immutable. 

The two most common consensus mechanisms are Proof of Work (PoW), introduced with Bitcoin and Proof of Stake (PoS). Cardano pioneered the first ‘provably secure’ Proof of Stake blockchain. Ethereum started out as a proof-of-work blockchain but transitioned to proof-of-stake in 2022.

3. The **networking layer** is where the nodes of the network talk to each other, facilitating the propagation of blocks. A block is a batch of transactions, but understand that almost everything on Cardano occurs as a result of a transaction. More about that later. This layer ensures data is distributed efficiently across the Cardano network. It is a peer-to-peer networking stack tailored for Cardano’s Proof-of-Stake system. This is also the layer which supports pipelining, multiplexing and various other protections against adversarial peers. 

4. The **scripting layer** sits atop and supports smart contracts. It enables programmable transfer of value and the development of DApps, or decentralized applications. Initially on Cardano, there was just the *Plutus Platform* which enabled developers to write smart contracts in Haskell which compiled to Plutus Core, a typed Lambda-Calculus that acts as low-level interpreted assembly code. Today, there are several high level languages which compile to Plutus Core, the most popular one being Aiken.


[^1]:CEHV’s Blockchain OSI Model Thesis, cehv.com/cehvs-blockchain-osi-model-thesis/
[^2]: What programming languages could match the OSI model layers?, quora.com/What-programming-languages-could-match-the-OSI-model-layers
