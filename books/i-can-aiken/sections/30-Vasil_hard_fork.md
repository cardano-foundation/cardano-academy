**Vasil hard fork**

Three important Cardano Improvement Proposals were implemented with the Vasil hard fork in September 2022. CIP 31 defined **reference inputs** which are a major step forward for how developers interact with UTxOs. A reference input is a transaction input associated with a specific transaction output. However, rather than spending the output, it just references it. A datum can be thought of as the data for your script, bits of data attached to outputs: you might store data like a user handle, or a restaurant order etc.

Reference inputs allow you to read the datum, or the data that’s stored at a UTxO, without consuming it and recreating it. This means that multiple DApps can read from the same datum simultaneously. This boosts concurrency and throughput dramatically. 

**Figure 31**: CIP 31 Reference Inputs  

We should pause and tip our hats to Ergo, pioneers in the UTxO space, who already introduced a similar concept called *data inputs* in 2020. 

CIP 32 defined **inline datums**. Before Vasil, the datum wasn’t stored on-chain. The hash (fingerprint) of it was stored on-chain and it was up to the developer to include it when they were interacting with the script. Since Vasil, the datum can be stored on-chain, eliminating the need for hashes and moving closer to a truly decentralized architecture. 

**Figure 32**: CIP 32 Inline Datums 

CIP 33 is about **reference scripts**. Plutus script references can be linked to transaction outputs, allowing them to be stored on-chain and reused later. It means you are no longer required to provide a copy of the script with each transaction, thereby reducing developer friction. Using the same script in several transactions decreases transaction sizes, boosts throughput and lowers script execution costs.

Reference scripts allow developers to put scripts on-chain and then, rather than include them in a transaction, they can instead include a pointer in the transaction that just references that script on the existing chain. That means that a user doesn’t need to have a copy of this script to interact with it. You just need to let people know the address it’s at, and then users anywhere can use the same script and point to it.

This enables a use case where a developer can put reference scripts on-chain and allow others to use them as a library. This allows anyone in the ecosystem to take libraries and make them available to the wider public.  

**Figure 33**: CIP 33 Reference Scripts

**Collateral**

Phase 2 validation must include **collateral**, a minimum sum of ada input from a PubKey address. This collateral protects against Distributed Denial of Service (DDOS) attacks, where malicious transactions flood the network. Failure of validation during Phase 2 forfeits this collateral. This rarely, if ever, happens, because invalid transactions are flagged well in advance. This is not the case on Ethereum, where the protocol allows transactions to consume significant gas and still fail, inflicting losses on the user with nothing to show for it. 

**Composability**

Another term you may run into when discussing smart contracts is **composability**. Composability is where developers reuse existing assets and reassemble them in unique ways to satisfy specific user requirements.

The elegant composability of its validators is one of the strengths of the eUTxO model. With the account-based model, smart contracts can call each other, but this can lead to a cascading effect of unintended side effects. 

As we covered earlier, the eUTxO model guards individual script outputs with their own validator, or validators.  Each script grants permission to spend the UTxO guarded by the validator, and this happens independently of anything else occurring around it. 

If the validators are well coded, and there are an increasing number of best practice guides available, different inputs can easily be combined in a single transaction, without the need of different scripts calling each other with unpredictable consequences.  

This ability to combine several swaps, for example, into one transaction does not require complex custom code like it does on other chains. It is a benefit inherent in the eUTxO design. The composability of eUTxO smart contracts often leads to unexpected user benefits as a byproduct of sound design decisions. 

For example, scripts can search for a transaction output based on its unique **UTxO reference**. No two UTxOs can have the same reference. Atomic-swap contracts, or flash loans, easily implement this capability and this makes them inherently secure against double-spending, UTxO contention and other attacks. 
