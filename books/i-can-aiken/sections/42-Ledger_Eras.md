**Ledger Eras**

Another consideration which impacts your validator is the **Ledger Era**. Think of it as a period in time that adds new functionality to the Cardano ledger. In the past we’ve had the Alonzo era, following the Alonzo hard fork, that introduced smart contracts to Cardano for the first time. This was Plutus V1. Then there was the Babbage era, which followed the Vasil hard fork, where Plutus V2 added new capabilities, like reference scripts and inline datums. We are now in the Conway era, since the Chang hard fork in September 2024. This brought us Plutus V3 with new features, such as governance actions, voting and exotic cryptographic primitives. 

Where are all these different names coming from? Cardano’s development phases: Byron, Shelley, Goguen, Basho, and Voltaire are named after poets, with the exception of Goguen, a computer scientist. Ledger eras are named after mathematicians and computer scientists in alphabetical order. It has become a tradition to name hard forks after people who made significant contributions to Cardano but who are sadly no longer with us: Vasil Dabov, Michael Chang and Matthew Plomin. You can delve more into the naming schemes in the documentation.[^1] 

**Ledger Language Version​**

So when you see Plutus V1, Plutus V2, Plutus V3 or just the abbreviations v3, etc., it refers to the **Ledger Language Version**. The ledger attaches the Ledger Language Version to validators in a transaction. If you have already inspected some code, you’ll see these as tags in the ‘toml’ file in the project’s root directory. More about this later.  

**Figure 47**:  icanaiken.toml file

This Ledger Language version only matters when you code up a validator, put it in a transaction and send it to the ledger. The ledger will provide different arguments and builtin functions to the validator, depending on the ledger language version. 

So for example, the governance features and cryptographic primitives required for ZK Rollups are only available with v3. At time of writing, the latest ledger language version offers more builtin functions than earlier ledger language versions, but this will change as the Plutus team plan to make all builtin functions available to all ledger language versions in future.  

When a new ledger language version is introduced with a new ledger era, the earlier versions remain in service, unchanged, as many validators previously written depend on older versions to continue working. So in conclusion, don’t think of Plutus V1, V2 and V3 as distinct programming languages. Instead just remember the ledger offers your validators different arguments depending on the version.  

It’s like your kitchen is stocked with different tools and ingredients depending on the version you have tagged. As you can’t whisk an egg with a cheese grater, choose wisely. 

**ScriptContext​** 

Each Plutus Core script also receives an argument called script context. This *ScriptContext* contains the transaction the script is validating, as well as its inputs, outputs, transaction fees, signatures, etc. The script context also has a script 'purpose' field, which we mentioned earlier. As the name suggests, the purpose describes exactly what the script is supposed to validate. 

**Figure 48**: A typical Aiken transaction illustrated 

A new era usually adds new fields but may also change existing fields. It’s not accurate, therefore, to say V3 is a superset of V2,. The script contexts for Plutus V1, V2 and V3 have different fields with different Haskell types. 

We’re just going to focus on the latest version, Plutus V3. It brought governance and voting functionality but also enhanced Plutus Core's cryptographic capabilities and enabled new possibilities. These new possibilities include the following:

- **CIP-1694** governance-related and voting features
- Interoperability between blockchains
- Support for porting Ethereum smart contracts to Cardano
- Sidechain bridges
- A 'Sum of products' which brings support for direct encoding of data types, meaning smaller, more efficient, scripts  

For more details on these new cryptographic primitives, see CIP-58 and CIP-85.

As we’ll see next, it is the UPLC component that is key to understanding how Aiken functions. It provides determinism and strong security assurances. Developers like predictable, reproducible settings, and Aiken builds on these foundations with a friendly developer experience and short iteration times. It's a joy, in this regard, as many developers have testified. We will focus on Aiken for the rest of this book.  

[^1]: Cardano Eras and Phases, docs.cardano.org/about-cardano/evolution/eras-and-phases/
