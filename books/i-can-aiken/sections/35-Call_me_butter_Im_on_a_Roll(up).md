**Call me butter, I’m on a Roll (up)!** 

Zero-Knowledge Rollups, or ZK Rollups, are a powerful scaling solution that can enhance the performance of DApps. By moving complex computations off-chain, ZK Rollups enable them to be executed much faster and consume fewer resources. It’s a little like a restaurant with a side kitchen where the sous-chef prepares fancier dishes and relieves the burden on the main kitchen. If you need a refresher on Layer 2 solutions, revisit *CBCA Module 2*.[^1] 

**Figure 36**: ZK Rollups

State changes are computed off-chain and subsequently validated on-chain using Zero-Knowledge Proofs. ZK Rollups thereby boost transaction throughput and lower transaction fees. They are able to do this as they inherit the security of the Layer 1 blockchain they are connected to for settlement. ZK Rollups then submit data subsets to Layer 1. This smaller data set is the result of processing a larger volume of data in Layer 2. ZK Rollups avail of the censorship resistance and security of the Layer 1 for final transaction settlement.

Unsurprisingly, Zero Knowledge solutions also reap the benefits of the eUTxO model. As discussed, UTxOs are independent, immutable objects, guarded by scripts and can be processed in a parallel, deterministic fashion.  

UTxOs are independent in that the validation of a transaction is predicated on its inputs and outputs only, which removes any need for a shared global state. 

**How transaction validation works**

The transaction itself, and its state are the validation inputs. The output is **True** or **False** based on whether the transaction is valid in the context of the state. 

As we covered earlier, unlike Ethereum, Cardano is predictable and deterministic. This key differentiator has far reaching impact, but nowhere more so than with ZK Proofs. Transaction validation is critical to maintain system integrity with ZK Rollups. Accurate and predictable validations protect against double-spending and the unauthorized minting of new assets. 

Similar to Ethereum’s Layer 1 mainnet, ZK Rollups on Ethereum’s Layer 2 also need to preserve a global state. Just as on Layer 1, this global state is impacted by every transaction, and the sequence of transactions is also a factor. Maintaining state in Ethereum ZK Rollups is managed by a centralized entity called a **sequencer** that basically reorders transactions to achieve a degree of determinism. This is often a single server updating the balances of user accounts.

**Figure 37**: The role of an Ethereum sequencer in a ZK rollup 

Users wishing to leverage ZK Rollups on Ethereum need to lock tokens that have been minted. This is done via a smart contract that locks the tokens and mints an equivalent amount in Layer 2. 

It is in Layer 2 that users submit transactions and these update the balances of user accounts there. Importantly, any state changes occurring in Layer 2 do not affect the global state of Ethereum at that time. 

In other words, the global state within the Ethereum network changes separately from the Layer 2’s state. If users want to leave Layer 2, it is a cumbersome process. They must unlock tokens secured by the Ethereum smart contract and withdraw them from the ZK Rollup. This initiates the burning of tokens in Layer 2 and the unlocking of an equivalent quantity of tokens in Layer 1. Any updates to the token ownership which occurred at Layer 2 are duly updated there too. 

A ZK Proof is required to withdraw tokens from a ZK Rollup. When a user wishes to move their tokens from the ZK Rollup back to Layer 1, they initiate a withdrawal. This request specifies the quantity of tokens to withdraw and the Ethereum destination address. 

The ZK Rollup system generates a Zero-Knowledge proof that validates the withdrawal request. This is proof that the user has ownership of the tokens on Layer 2 and that they are unspent. The ZK Proof is then submitted to the Ethereum smart contract. Once the smart contract verifies the proof is valid, the requested amount of tokens are unlocked and sent to the user’s Ethereum address. While the balances in Ethereum and ZK Rollup are in touch with each other, they are not always equal and they function independently. 

**Rolling it all together**

ZK Rollups utilize cryptographic proofs to attest to the validity of state transitions that result from batched transactions. This allows the Ethereum smart contract to verify the new state root without re-executing individual transactions. By maintaining an account-based model and full EVM compatibility, ZK Rollups facilitate seamless migration of your existing DApps from mainnet,  and this enhances scalability and efficiency without code modifications. 

Most of the research and innovation in the Ethereum ecosystem has been in ZK Roll Ups over the past few years, with fading efforts to pursue sharding. 

[^1]: Cardano Blockchain Certified Associate, academy.cardanofoundation.org/
