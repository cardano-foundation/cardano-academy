# Cardano Stack

Although there have been several attempts, such as the 11-layer model, there is still no canonical standard for the blockchain stack. As most new arrivals from the Web2 world are familiar with the ubiquitous OSI model, it makes sense to map the Cardano blockchain stack similarly.

**The Four Layers of the Cardano Blockchain:**

1. Lying at the bottom is the settlement layer which hosts a financial distributed ledger derived from formal specifications. This is the foundational layer which tracks the movement of ada and native assets from one wallet to another and records transaction details.

2. Next to bottom is the consensus layer which is crucial for maintaining the security and robustness of the network. Here you’ll find the Ouroboros algorithm which achieves consensus on the state of the ledger. Bear in mind, the operation of any consensus mechanism is based on three key properties: safety, liveness, and finality. Safety is sometimes explained as “a guarantee that nothing bad will happen”. A less vague description is that honest nodes will have the same view of the blockchain. Liveness is a guarantee that all validators will reach consensus on a value, so new transactions are regularly added to the blockchain. Finality is the point at which a blockchain transaction is widely accepted as irreversible and immutable. 
The two most common consensus mechanisms are Proof of Work (PoW), introduced with Bitcoin and Proof of Stake (PoS). Cardano pioneered the first ‘provably secure’ Proof of Stake blockchain. Ethereum started out as a proof-of-work blockchain but transitioned to proof-of-stake in 2022.

3. The networking layer is where the nodes of the network talk to each other, facilitating the propagation of blocks. A block is a batch of transactions, but understand that almost everything on Cardano occurs as a result of a transaction. More about that later. This layer ensures data is distributed efficiently across the Cardano network. It is a peer-to-peer networking stack tailored for Cardano’s Proof-of-Stake system. This is also the layer which supports pipelining, multiplexing and various other protections against adversarial peers. 

4. The scripting layer sits atop and supports smart contracts. It enables programmable transfer of value and the development of DApps, or decentralized applications. Initially on Cardano, there was just the Plutus Platform which enabled developers to write smart contracts in Haskell which compiled to Plutus Core, a typed Lambda-Calculus that acts as low-level interpreted assembly code. Today, there are several high level languages which compile to Plutus Core, the most popular one being Aiken.

**Questions**

1. Which of the following is NOT a layer in the Cardano blockchain stack?
A) Settlement layer
B) Consensus layer
**C) Application layer**
D) Scripting layer

2. What is the purpose of the scripting layer in the Cardano blockchain stack?
A) To handle network communication between nodes
B) To ensure the security and robustness of the network
C) To track the movement of ada and native assets
**D) To enable the development of smart contracts and decentralized applications**

3. Which consensus mechanism is used by the Cardano blockchain?
A) Proof of Work (PoW)
**B) Proof of Stake (PoS)**
C) Proof of Human (PoH)
D) Practical Byzantine Fault Tolerance (PBFT)

4. Which consensus protocol is currently implemented on Cardano?
**A) Ouroboros (Praos)**
B) Hydra
C) Mithril
D) Ouroboros Leios

5. What programming language was initially used to write smart contracts on Cardano?
A) Aiken
B) Solidity
**C) Haskell**
D) Python

6. What is Plutus Core in the context of Cardano?
A) A high-level programming language for smart contracts.
**B) A low-level language acting as assembly code for smart contracts.**
C) The consensus algorithm used by the Cardano blockchain.
D) The networking protocol used by Cardano nodes.

7. Which consensus mechanism is utilized by the Cardano blockchain?
A) Proof of Work (PoW)
B) Proof of Stake (PoS)
**C) Ouroboros** 
D) Practical Byzantine Fault Tolerance (PBFT)

8. What are the three key properties of a distributed consensus mechanism?
A) Security, efficiency, and scalability.
**B) Safety, liveness, and finality.**
C) Centralization, immutability, and transparency.
D) Speed, cost, and energy efficiency.

9. What is the primary function of the settlement layer in the Cardano blockchain stack?
A) To execute smart contracts.
B) To manage communication between nodes.
**C) To track the movement of ada and native assets.**
D) To ensure all nodes agree on the state of the blockchain.
