*** uodate to "layer 2" roll ups  rather than ZK rollups when tlaking generally then be specific when talking about projects, ie. zk vs optimistic, etc

**ZK Roll Ups on Cardan**

Cardano's deterministic transaction model offers a significant advantage for ZK Rollups. Unlike Ethereum, where transaction outcomes depend on the global state at the time of execution, Cardano's UTxO model allows for predictable outputs during transaction construction off-chain. In other words, the strengths of the UTxO model in Layer 1 can be transferred to Layer 2. This eliminates the need for sequencers in ZK Rollups, which in turn promotes decentralization and potentially removes reliance on external data availability layers.[^1] 

Even without the need for centralized sequencers and transaction batching, it’s still necessary to relay the state of Layer 2 to Layer 1 to maintain system integrity and consistency. Although Cardano doesn’t need sequencers to achieve determinism, Layer 2 still inherits its security from Layer 1.  UTxO’s deterministic behavior opens up new implementation possibilities. It should be possible to develop decentralised ZK Rollups more efficiently than what we’ve seen with an account-based model. 

**Figure 38**:  UTxO model vs Account model   

So the design decisions we described earlier have come home to roost for both chains. Cardano focused on transaction determinism, local state and security which are key requirements for implementing ZK Roll Ups smoothly compared to account-based blockchains. Vast sums of venture capital money have flooded into the Ethereum ZK Roll Up ecosystem. However, most of the solutions are centralized sequencers - glorified multi-sigs, and many of these have fallen victim to hacks and exploits. 

The strength and security of ZK Rollups rely heavily on the liveness and security of the underlying Layer 1. No blockchain has a more impressive record in this regard than Cardano. Second only to Bitcoin in uninterrupted uptime since 2017, Cardano is the most stable and reliable chain offering smart contract capability. 

On Sunday, September 1, 2024, the Chang hard fork introduced advanced cryptographic primitives, the building blocks for ZK Roll Ups. It is a little like a chef being given access to new exotic spices. It enables meals and cuisines not possible before.

There are several projects working on new Zero Knowledge solutions. For example, Midgard is differentiated from existing Layer 2 solutions. It has no reliance on centralized systems and operates without a centralized sequencer, custodial requirements or multi-signature dependencies. Not just a Layer 2 Roll Up in its own right, it’s a framework for building other Layer 2 solutions. 

Although relatively late to the ZK Roll Up space, Cardano’s eUTxO model is more suited to support truly decentralized, trustless and performant Roll Up solutions, and in ways not possible on other chains. As Cardano’s fledgling ZK Roll up ecosystem starts to flourish, the foresight of earlier decisions will become more apparent. 

**Roadmap priorities** 

Implementing Input Endorsers will require structural changes to the core protocol and ratification from an on-chain vote. Many community members feel ZK Roll Ups should be a greater priority on the roadmap. Many of these debates will take center stage as Cardano turns on its on-chain governance mechanisms and the treasury becomes more accessible in 2025. 

We are starting fresh with a new funding process in 2025. Even established initiatives like *The Cardano Summit* and *Project Catalyst* must submit proposals for funding to be voted on by ada holders.

[^1]: Data availability layer is a foundational layer in blockchain which ensures data is reliably stored and accessible for users and DApps
