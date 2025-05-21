The UTxO set is made up of all UTxOs created as transaction outputs that are eligible to be spent in future transactions. This UTxO set is therefore a subset of all UTxOs which make up the blockchain’s history since the Genesis block on Saturday, September 23, 2017.

Validating a new block requires the current state of the blockchain. The collection of all unspent UTxOs, the UTxO set, captures this. So, as we are leveraging the UTxO set to validate new transactions, it’s not necessary to account for the entire history of the blockchain. That said, obtaining the active set of UTxOs usually involves processing the entire history of the blockchain, going all the way back to the Genesis block. 

**Figure 21:**  State before a block is added to a UTxO-based blockchain 

**Figure 22:**  State after a block is added to a UTxO-based blockchain 

The architecture of the UTxO model, along with its transaction validation process, makes life easy for nodes to identify and prevent potential double-spending. The UTxO set, made up of immutable, single-use objects, affords parallelism within the network. Transactions are validated independently of each other, similar to how UTxOs are consumed separately. Another benefit a UTxO system inherits is that it can validate transactions locally prior to submission. Developers can be assured in advance their DApp’s transactions will also pass the network validation later. 

A DAG, directed acyclic graph, represents a complete, auditable history of all transactions which have ever occurred on Cardano. Developers can audit  eUTxO smart contracts more simply because they need only assess the validation script, which has only a **local scope**. 

**Figure 23:**  UTxO model is a DAG (direct acyclic graph) 

When you spend a UTxO, the smart contract validates the transaction. Smart contracts are often described as autonomous objects which run automatically, but UTxO validators are more like *guards*. This ensures DApps behave as they should. Instead of striving for an aspirational *world computer* with complex and cascading smart contracts, Cardano aims to optimize on-chain smart contracts for scalability with a prudent level of expressiveness. 
