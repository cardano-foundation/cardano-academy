**Won’t somebody please think of the developers?**

Most Web3 developers are more familiar with the account-based model on Ethereum and EVM-compatible chains. The eUTxO model is quite a paradigm shift from an Account-based model. Existing DApps created on Ethereum and similar blockchains cannot simply be ported over for use on eUTxO platforms. It’s best to start from scratch. 

**Figure 40**: Web2 vs Web3 typical architectures 

The eUTxO model allows for greater flexibility with smart contracts through off-chain computation. Compared to eUTxO, the Account model executes all smart contract logic on-chain. This inevitably leads to scalability issues as the blockchain bloats when the number of transactions increases. However, the eUTxO model offers new design opportunities, as most of your DApp’s smart contract logic can be moved off chain. It just executes the validation process on the blockchain and thereby improves efficiency and scalability. 

**Figure 41**: Typical Cardano DApp architecture (~70/30% split off/on-chain)

An account-based blockchain can get congested quickly, as gas fees spike when the user base is active during peak times. The issue of scalability is one of the main factors why Ethereum has pushed so much computation, and off-chain code, to Layer 2 in recent years. Ironically, the solutions Ethereum is exploring to unclog the Layer 1 mainnet mimic those of eUTxO in practice. 

**Figure 42**: Ethereum global state

In addition to the **on-chain** code, one typically needs the accompanying **off-chain** code and services to perform tasks like building transactions, submitting transactions, deploying smart contracts, querying for available UTxOs on the chain, etc. 

A full suite of solutions is available for review under the ‘Showcase’ section of the Cardano Developer Portal. Some popular frameworks include cardano-transaction-lib, Lucid Evolution and Mesh JS. All are based on the Cardano API,[^1] a low-level API that provides the capability to do off-chain work with a local running node.  

Developers need to use design patterns that reduce the amount of work done on the blockchain itself to minimize transaction fees. This means favoring off-chain computation and storage whenever possible. But how much data?  And what data types need to be on-chain? 

This conundrum is not chain specific. Design patterns for web3 are different to web2, but Cardano’s eUTxO model affords developers more flexibility to shift a lot more of their DApps’ functionality off-chain. It takes some research and experience to understand what data to keep on-chain vs off-chain. What criteria do you use to decide? How do you need to interact with on-chain data? Is the data sensitive? Should the data be queryable on a public blockchain? Are there plans in place for rollbacks, or even hard forks? 

Don’t despair as there is support on hand from the Cardano Foundation, who recently published a *Whitepaper Template to Support Cardano’s MiCA Compliance*.[^1] The template is designed to help Cardano projects navigate the complexities of MiCA (Markets in Crypto-Assets Regulation) and support compliance with its disclosure requirements. 

The only thing that can possibly change on a eUTxO blockchain is the UTxO set. Individual UTxOs are immutable. You can only create new ones. When an output is created, it can’t be modified, only spent or consumed. Similarly, the other data structures like the datum and redeemer are also immutable. This makes Cardano attractive for functional programmers, as many of the concepts are similar. For example, there is no global state in functional programming either.  

Given the conclusions of much of the research, and the properties of eUTxO, it was not surprising that Haskell was Cardano’s primary programming language for many years. Cardano itself is implemented in Haskell. It is the language used on the Plutus Framework and taught through several iterations of the Plutus Pioneer Programs. As a functional programming language, Haskell offers strong static typing and expressiveness. These characteristics are valuable in modern languages because they help reduce errors and simplify the process of turning complex requirements into working programs. 

Though there is a paradigm shift for those coming from account-based blockchains, we hope you are beginning to see eUTxO smart contracts can, if architected well, be simpler than their Solidity equivalents. Shortly, we will chart the rise of Aiken. We’ll look at how it became the dominant smart contract programming language on Cardano ahead of Plutus, and we’ll see how easy it is to write validators in Aiken.

[^1]: Cardano API, github.com/IntersectMBO/cardano-api
[^2]: Whitepaper Template to Support Cardano’s MiCA Compliance, cardanofoundation.org/blog/whitepaper-template-cardano-mica-compliance
