# UTxO State Transitions

Each individual transaction can transition the UTxO set to a new state. But in practice this is unsustainable. For a large user base transacting simultaneously, all users must be in sync on the current state. 

Architecting a consensus protocol that keeps all nodes in sync is non-trivial when state transitions occur on an individual transaction basis. There is only a certain time interval between blocks. Currently there are 20 seconds for network nodes to update their UTxO set based on the latest block. As a result, transactions are bundled into blocks and each new block represents a state transition.

## UTxO Example​ 
Let’s start with a UTxO state transition for a single transaction. 
Let's pretend I want to transfer 10 ada to your wallet, and I have a single UTxO, worth 15 ada. I create a transaction which consumes my 15 ada UTxO as its input. 

To spend the UTxO, I need to satisfy the conditions to unlock it. I must provide my digital signature as the owner of the UTxO. Next, my wallet creates transaction outputs. A new UTxO worth 10 ada is sent to your wallet’s receive address, and another UTxO worth 4.9 ada is returned to my receive address as change.

For both outputs, the spending conditions are also defined in the transaction. You may have spotted that the sum of outputs doesn’t equal the total consumed input. This difference is the transaction fee. In this example, the transaction fee is 0.1 ada and is calculated by the wallet according to the amount of data recorded on-chain. 

For our analogy, this transaction would have involved me sending you a voucher, and receiving back a smaller voucher as change. My input voucher is torn up, or redeemed, and newly created vouchers are output. Everyone, including the protocol, gets what’s owed. I get a 4.9 ADA voucher as change, you get a new 10 ADA voucher and the protocol gets its transaction fee voucher of 0.1 ada.

## UTxO Model: Key takeaways
Note that once a transaction UTxO is newly created as an output of a transaction, it can’t be updated or changed until it is spent in a future transaction. Once it is spent, it is completely spent, or consumed in full, and a new UTxO is created as output of the new transaction. In other words, UTxOs are independent and immutable, which enable users to submit transactions in parallel. This means faster verification and validation, and this boosts scalability.

Transaction validation relies on UTxO’s simple and predictable features. The global state is represented by the active bunch of UTxOs, or the UTxO set. When a node accepts a new block, each transaction has UTxO inputs from the UTxO set, and the UTxOs consumed are removed from the UTxO set. A new global state then emerges. The range of possible outcomes is more predictable than with an Account-based system, with no surprises making execution safer. Removing consumed UTxOs like this helps to reduce blockchain bloat, and this in turn results in more efficient storage.

Each network node keeps its own UTxO set. A majority of nodes agreeing on the same UTxO set establishes consensus and this preserves the same transaction history of the blockchain. Note that the network does not transmit data immediately. There is a slight delay.

## Questions

In the UTxO model, what happens to a UTxO once it is spent?

A. It can be reused in future transactions
B. It is partially consumed
**C. It is completely consumed and removed from the UTxO set**
D. It is transferred to a new owner

How does the account model handle state transitions?

A. Each transaction triggers a state transition
**B. Transactions are bundled into blocks, and each block triggers a state transition**
C. State transitions occur only when a new user joins the network
D. State transitions are managed by a central authority

What is the primary role of a smart contract on Cardano?

A. To execute complex computations
B. To facilitate cross-shard communication
C. To manage user accounts
**D. To validate transactions**
