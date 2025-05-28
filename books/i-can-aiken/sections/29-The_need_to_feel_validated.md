**The need to feel validated** 
We said Cardano network nodes validate transactions, but how does this validation take place? It occurs over two *phases*.

**Phase 1**

The first phase consists of a few basic initial checks. Unlike Ethereum, there is no fee if a transaction fails early.  

The first check verifies if the transaction inputs are unspent. Transaction inputs are being spent all the time, so it’s possible a UTxO input is spent and thus unavailable during the period between when a transaction is constructed and submitted to when a node validates it. The transaction would then be invalid. If multiple transactions try to spend the same UTxO, this is known as **contention**. We’ll discuss some techniques to mitigate this risk later.

The next check confirms the spender has enough funds to cover the transaction. Specifically, that the sum of the input values must, at least, equal the sum of the output values plus the transaction fees. This check is predictable, or deterministic, and can be confirmed before a transaction is submitted.

As there is no concept of network time protocol (NTP) on a blockchain, a common question is 'how does Cardano deal with time?' There is a research paper outlining how Ouroborus Chronos solves this issue at the consensus layer. At the scripting layer, we need only consider that transactions include a **validity interval**. This is the window of time during which a transaction can be deemed valid. The interval can be unrestricted or have very precise slots. So this is another quick check the node performs to verify if the transaction is valid. 

As part of Phase 1, transactions can also be checked for an arbitrary number of **required signatures** to be present.

**Phase 2**

Phase 2 of validation, which only happens after all Phase 1 checks are passed, is more rigorous with harsher penalties. This phase can be done off-chain, before submitting the transaction on-chain. This is a big win for efficiency and reducing on-chain bloat. Think of Phase 2 as being like a dress rehearsal, where all scripts are executed under the same conditions as opening night. A transaction might have multiple script inputs, in which case, they must all return **True** for the transaction to be valid. 

Although possibly counterintuitive, the transaction itself needs to include all scripts that need to be run during Phase 2. This would result in a lot of repetition and replication, causing the chain to bloat significantly. The following features were introduced during the **Vasil** update in 2022 to mitigate these risks.
