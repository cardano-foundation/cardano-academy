# Account-Based State Transitions

The account model records all user balances as one global state. This means the state of all accounts, private keys and smart contracts, along with their associated balances of various assets.

Whereas only the addition of new UTxOs, or transaction outputs, extends the UTxO global state, the account model updates the list of accounts and all their balances change.

Similar to the UTxO model, a transaction can initiate a state transition of the blockchain with the account-based model. This does not happen for every single individual transaction, however, as that would risk an inconsistent state. Instead, transactions are also bundled into blocks in the account mode. For each new block, the system transitions to a new state.

Lets look at a straightforward example of a single transaction that triggers a state transition. In this elementary example, Alice, Bob, Fred and Charlie have state n starting balances of 100 eth, 10 eth, 10 eth and 10 eth, respectively. Alice transfers 10 eth each to Bob, Fred and Charlie. The respective balances then update to 70 eth, 20 eth, 20 eth and 20 eth in state n +1.

## Compared to UTxO 
The UTxO model is a validation model. Transactions specify set results of a state transition and create new unspent transaction outputs, UTxOs. These are then available as inputs for future transactions. Network nodes then check if the input is indeed unspent and if any other spending conditions are satisfied. For example, are the required signatures present?

In contrast, the account model is closer to a computational model: users submit transactions which tell the network nodes what the state transition should look like. The new state is then created based on these instructions.

This might seem like a subtle difference but it has broad ramifications for scaling solutions like state channels and sharding. Such early design decisions ripple out with far reaching consequences in a decentralized, distributed system like a blockchain.


