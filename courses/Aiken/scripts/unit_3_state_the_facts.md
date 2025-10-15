# State the Facts

So to recap, a blockchain is a distributed ledger where transactions, or state transitions, are processed by appending new blocks to a blockchain. There’s that word ‘state’ again, and it’s a term you will also encounter frequently when discussing on-chain smart contracts.

State refers to the current status of all data stored on the blockchain. ‘Stateful’ and ‘stateless’ describe what, if anything, a DApp records about previous sessions. Generally, stateful DApps retain data, remembering what went before. They keep track of the ‘state’ of the system, while stateless DApps don't.

A blockchain can be seen as a special kind of replicated state machine. The 'state' of a blockchain is the current status of all accounts, balances, and data stored on it. The inputs are transactions. When someone sends cryptocurrency, interacts with a smart contract, or adds data to the blockchain, they are providing an input. These transactions trigger changes, or transitions, in the blockchain's state. 

A transaction that transfers coins will change the balances of the sender and receiver, thus changing the overall state. The state machine is 'replicated' because every node in the blockchain network maintains a copy of the entire state. This ensures redundancy and makes the system resilient to failures.

Determinism is another concept that you will hear in many discussions. In general, if an outcome is predictable, we say the process is ‘deterministic’. In systems design, predictable outcomes make life easier for developers. A blockchain strives to be, and in most cases is, deterministic. 

Given the same starting state and the same set of transactions, every node aims to eventually arrive at the exact same final state. This is critical to system consistency and integrity. As we’ll see later, transactions can be deemed deterministic or non-deterministic.

**Questions**

1.  What does "state" refer to in the context of blockchain?
A. The physical location of a blockchain node
**B.The current status of processed data stored on the blockchain**
C. The type of consensus mechanism used by the blockchain
D. The programming language used to write smart contracts



