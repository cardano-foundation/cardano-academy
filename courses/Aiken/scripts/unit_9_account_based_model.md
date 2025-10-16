# Account-Based Model

The account-based model works differently from UTxO chains when tracking blockchain state. With account-based models, the blockchain state maps each account with the amount of assets the account owns. There are two types of accounts: user accounts and contract accounts. 

The state of the ledger is updated to reflect changes in account balances after transactions are executed. Transactions modify a balance by either deploying a new account or updating an existing account balance. Transactions can transfer assets only if the sender account signs the transaction, proving ownership of all the assets to be transferred. 

The account-based model is considered stateful. A little like a global variable in programming parlance, Ethereum maintains a global state on the blockchain. This state consists of a collection of accounts, each with its own balance, code (if it's a contract account), and storage. 

Unlike Bitcoin's UTxO model where the state is implicit, Ethereum explicitly stores the state of each account on the blockchain. This means every node in the network needs to maintain a copy of this entire state. When a transaction occurs on Ethereum, it directly modifies the state of the accounts involved.

For example, if I send you 10 ETH, the state is updated to reflect the change in both our balances. The transaction specifies the sender account, the recipient account, the amount of ETH to be transferred, some optional data and some gas. 

Think of gas as transaction fees users pay on Ethereum to conduct transactions and execute smart contracts. When a transaction is processed, the network checks that the sender's account has enough balance to cover the transfer requested and the gas fees required. If the recipient is a contract account, the transaction triggers the execution of the contract's code.

Another consideration is that Ethereum block producing nodes process transactions sequentially because each transaction can potentially affect the state of any account on the network. To ensure the integrity of the system, it's therefore necessary to lock the global state for each validation, so just one transaction can be processed at a time. If the global state was not locked like this, there could potentially be double-spending, race conditions and inconsistencies.

Every new transaction added to the block changes the current global state of the node. When a new block is shared on the network, each validator must individually verify the transactions within it. Checking each transaction one by one in the original order, they must follow the exact same sequence used by the node that created the block.

**Questions**

1. What type of accounting model does Ethereum use?
A) UTxO
**B) Account-based**
C) Hybrid
D) Proof of Work

2. How does the account-based model differ from UTxO?
A) It is more secure
B) It is more private
**C) It maintains a global state of accounts and balances**
D) It is less efficient
