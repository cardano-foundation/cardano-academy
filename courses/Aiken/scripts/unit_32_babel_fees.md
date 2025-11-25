# Babel Fees

Another byproduct of the eUTxO multi-asset model is the Babel fees research stream. Babel fees is an innovative feature that will allow transaction fees to be paid in the native currency of a given chain, so there’s no requirement to necessarily pay in ada. It will be a huge boost to user experience and interoperability.  

Babel fees are named after the Babel fish, a creature in Douglas Adam’s book, The Hitchhiker’s Guide to the Galaxy, that enables you to hear any language translated into your own. Despite the galaxy’s many varied languages, this vision described in the book, of global translation, enables meaningful communication.

Cryptography and game theory have a history of making the seemingly impossible achievable. Cardano’s Extended UTxO (eUTxO) architecture enables this solution because of how native assets function on the platform.

As discussed, Cardano’s native asset support means user-defined tokens may be generated using a minting policy, and they are treated the same as ada on the ledger. Creating a valid transaction requires the consumption of one or more UTxOs. On Cardano, a transaction may hold more than simply ada; it can also handle a token bundle containing numerous distinct tokens, both fungible and non-fungible. It is therefore feasible to use a single transaction that contains multiple UTxOs to transfer many distinct tokens.

The ledger’s transaction fees are priced in ada based on a function fixed as a ledger parameter. The costs necessary for a successful transaction may be anticipated accurately prior to execution–a key strength of Cardano’s eUTxO’s architecture. This is a unique property that other ledger configurations do not have. Assuming there is enough liquidity and demand, a user can use these user-defined tokens to pay transaction fees.

The hotly anticipated implementation of babel fees is underway with the “Nested Transactions” CIP. This new feature will allow multiple related transactions to be bundled and validated together, ensuring atomicity of the transaction on-chain. In early 2025, FluidTokens implemented a smart contract-based version of Babel Fees known as Aquarium.

Returning to our analogy, think of Babel fees as allowing you to pay for your meal with any accepted voucher, token or currency. The experience will be the same if you are paying in either loyalty tokens, “OneForAll” vouchers or ada.

## Questions

1. What is the purpose of nested transactions in the implementation of Babel fees?

A. To ensure the privacy of transactions
B. To increase the speed of transaction processing
**C. To ensure the atomicity of transactions**
D. To reduce the cost of transaction fees


