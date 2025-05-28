One of the biggest flaws with Ethereum is the unpredictability of the global state at the time of transaction validation. This can lead not only to failed transactions but also broader uncertainty: even as a transaction is being constructed, there’s no way to know the outcome. The global state during transaction validation is likely to be different from the state during transaction construction. In the time between transaction submission and validation, account balances of the parties may also have changed.

When a transaction is executed, the EVM calculates the **new state** based on the **current state** and the transaction. This updated new state then becomes the current state for the next transaction. In this way, the state of the Ethereum blockchain is constantly evolving with each transaction.

The account balances themselves are inputs to transactions and the balances can be updated by different sources continuously. This means from the time a transaction is submitted to the time it is validated, the balance itself can have changed. Inputs are not predictable, or deterministic, as they are with UTxO where you can run an accurate test locally to verify transactions will pass validation later. 

When you consider all these factors, and the fact that the global state is represented by the current state of **all** accounts and smart contracts, you should be coming to the realization that this is not a trivial process.

**Figure 13:** Ethereum transaction

Smart contracts further reinforce the stateful nature. They store and modify data within their own storage, which is part of the overall Ethereum state. Every node needs to be aware of the current state to validate transactions and execute smart contracts. 

Early design decisions have long-term repercussions. While complex DApps are running today on Ethereum, scalability is still an issue as the state grows larger. The Ethereum community has acknowledged this issue by actively working towards alternatives like stateless clients and Layer 2 solutions. More about this later.
