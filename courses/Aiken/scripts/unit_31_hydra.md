# Hydra

Hydra was the first scaling solution to leverage eUTxO’s design. The ‘’Hydra: Fast Isomorphic State Channels’’ paper introduced Hydra, an isomorphic multi-party state channel. State channels are a layer 2 solution for improving the throughput and latency of a blockchain. They extend the concept of payment channels to also support smart-contracts over off-chain channels. Channel participants can, in addition to traditional payments, run scripts to handle complex logic off-chain before committing the result back to the Layer 1.

What are isomorphic state channels exactly? Well Iso is a prefix meaning equal. Isometric means equal measurements. Morphic relates to shape or form. So isomorphic means having the same structure and properties.

Why is this significant? Isomorphism enables Hydra to allow the same code to be used both on-chain and off-chain. Hydra also leverages the fact that independent parts of the transaction graph can be processed in parallel.

Hydra’s real world effectiveness has been demonstrated recently by powering the classic computer game Doom, which originally came out back in 1993, with a new release due in 2025. Doom running on Hydra through a classic arcade console has been a popular attraction at Cardano conferences answering an emphatic “yes” to the common question in the gaming world “can it run Doom?” You can look in on Hydra’s development progress at the website: hydra.family here. 

If we were to consider the Layer 1 mainnet only, every game state transition would need a transaction which could become expensive, slow and ineffective, but on Hydra, multiple games could be played fast, in parallel with almost zero costs for game transitions while the final outcome of the game can be written back to the Layer 1. 

Returning to our restaurant analogy, if the Layer 1 mainnet is the kitchen which can handle a certain throughput of dishes, you can think of Hydra channels as like a fleet of food trucks that can prepare and deliver the same quality meals in parallel.

## Questions

1. What is Hydra in the context of Cardano?

A. A consensus mechanism 
B. A governance system that allows stakeholders to vote on proposals
**C. A layer 2 scaling solution that uses state channels**
D. A smart contract language that enables complex logic

2. What does isomorphic mean in the context of Hydra state channels?

A. Having different structures but the same properties
B. Having the same shape but different sizes
**C. Having the same structure and properties**
D. Having variable shapes and sizes


