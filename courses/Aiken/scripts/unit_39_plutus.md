# Plutus
We can’t talk about Aiken until we explain its relationship with Plutus. As we mentioned, Plutus was the primary programming language for writing smart contracts on Cardano in the early years. When we say Plutus, we really mean Haskell code running on Plutus Platform.  

Haskell was the obvious candidate as much of the rest of Cardano’s infrastructure, libraries and tooling are also written in Haskell. It is a functional programming language with strong static typing, high expressiveness, mathematical rigor. It also supports the kind of formal verification often used when developing mission-critical applications where failure is not an option.

When people mention Plutus, they could be referring to any of the following three components: 
- **PlutusTx** is a plugin for compiling Haskell to Plutus Core. Note that PlutusTx was subsequentally renamed Plinth. 
- The **Plutus Application Framework** is a suite of tools for writing smart contracts in Haskell.
- **Untyped Plutus Core (UPLC)** is the machine code for the Cardano ledger, the lowest level representation of a smart contract that runs on-chain.

There is more nuance to consider, however, when using Haskell in a blockchain setting. Haskell first appeared in 1990 and wasn’t built specifically for blockchains. In short, the Haskell code running on Cardano through the Plutus virtual machine is a small subset of the mainstream, Turing-complete, Haskell that has been around for decades. The wider ecosystem of reusable packages and code libraries familiar to Haskell developers are not available. The PlutusTx compiler will alert you if you try to use anything that is not supported.

Many developers report a steep learning curve with Plutus and a tedious set up experience with outdated tooling. For example, because it is an embedded Domain Specific Language, it requires you to recompile all libraries each time you test a new version of your smart contract. As space is at a premium on the blockchain, Haskell, along with most mainstream languages, struggles as it is not tailored to the unique execution model imposed by the ledger.
Questions

1. What is the lowest level representation of a smart contract on Cardano?

A)  Haskell 
**B) Untyped Plutus Core (UPLC)**
C) PlutusTx
D) The Plutus Application Framework

2. What does UPLC stand for?

A) Universal Programming Language for Cardano
B) Unified Plutus Ledger Compiler
**C) Untyped Plutus Core**
D) User-defined Plutus Contract Language
