# Ouroboros Leios and Peras

While Hydra’s focus is to enable faster transaction processing on layer 2, it doesn’t address the throughput and latency of the Cardano layer 1 mainnet. This led to the development of Ouroboros Leios and Peras.

Perhaps the most ambitious and important research stream is that of Ouroboros Leios, also known as Input Endorsers. The implementation of input endorsers is non-trivial and will require major changes to the protocol which will potentially impact the entire stack. The update will only take place if ratified by an on-chain governance vote.

The improvements will mean much shorter block propagation times and throughput. 
Input endorsers will track all submitted transactions and batch them into pre-constructed blocks. This means there are two types of blocks, those that contain the transactions and those that achieve consensus. Blocks focused on consensus will reference the pre-constructed blocks. The key point is that these pre-constructed blocks can now be constantly streamed without the need to wait for consensus to be achieved.

Crucially, Input Endorsers is only possible due to the UTxO model that will enable features like payload decoupling, concurrent processing and decentralized computation. 

To dig deeper, go to the research paper. 

While Leios is designed to achieve optimal throughput levels, Ouroboros Peras focuses on enabling fast finality. Both protocols rely on stake-based voting but will operate separately. Peras is seen as less complex to implement, so it is expected to be introduced ahead of Leios.  

Peras extends the Ouroboros Praos protocol, which addresses the challenge of transactions’ settlement time–the point in time when the chance of a transaction being rolled back is considered negligible. Faster settlement times will boost Cardano’s security, usability and efficiency. Peras is the first time the Cardano community has adopted a more collaborative approach, whereby the protocol update has been drafted first as a CIP before the publication of the research paper. 

## Questions

1. What is the main focus of Ouroboros Leios?

A. To enable fast finality of transactions
B. To improve the security of the blockchain
**C. To increase throughput on Cardano**
D. To reduce the energy consumption of the network

2. What is the main focus of Ouroboros Peras?

A. To enable the use of zero-knowledge proofs
B. To improve the scalability of the blockchain
C. To increase the decentralization of the network
**D. To enable fast finality of transactions**


