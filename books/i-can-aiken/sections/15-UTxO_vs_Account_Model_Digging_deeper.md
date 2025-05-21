**15. UTxO vs Account Model: Digging deeper** 

Most blockchains leverage either the UTxO or account model to track who owns what. The UTxO and the account model function differently in how they record state and manage transitions between states. For example, the UTxO model is more granular than the account based model, as it tracks each individual UTxO and not just total balances. 

**Figure 15:** UTxO model vs Account model  

**Recording the State**

​The transfer of assets between addresses is recorded as a **directed acyclic graph[^1] (DAG)** in the UTxO model. The account model, on the other hand, resembles a traditional database of user balances.

A directed acyclic graph (DAG) is a directed graph with no directed cycles. It consists of vertices and edges, with each edge directed from one vertex to another, so following those directions will never form a closed loop.

In simpler terms, think of a DAG as a way to visualize and organize information that has a specific flow. Imagine a bunch of points, called vertices or nodes, connected by arrows, called **edges**. It is **directed** in that the arrows only go one way, showing a relationship between the points. It is **acyclic** in that you can't follow the arrows in a loop and end up back where you started. It's a one-way flow chart with no circular paths. This is useful for representing things that have a clear order or dependency.

On the left, note the directed acyclic graph does not permit circular relationships between the UTxOs. In the graph, each row represents a **state** and each transaction output comprises one or more newly created UTxOs. A transaction can have multiple edges coming from a transaction output. In keeping with this, an **unspent** transaction output does not have any edges coming from it. In our graph on the left, UTxOs labelled 1, 5, 6, 7 and 8 represent **unspent** UTxOs.

The account model on the right should look more familiar to anyone with a bank account. For each new block appended to the blockchain, the global state updates based on the transactions batched in that block.  

**Figure 16:** Ethereum Global State 

The entire graph of transaction outputs, both spent and unspent, represents the global state in the UTxO model. On the other hand, the account model represents the global state as being made up of only the current set of account balances. The key difference is that the account model tracks all user balances everywhere, and the UTxO model records only transaction receipts. The active UTxO set is the set of unspent UTxOs **only**. 

UTxO calculates your wallet balance by counting all available unspent transaction outputs at your **'receive'** address. There is no concept of individual accounts, just individual transactions batched in blocks. Many wallets will show you a breakdown of the UTxOs you hold in said wallet.

We can compare this to a user holding certain amounts of vouchers worth any nominal value. That user's balance equals the sum total of the vouchers in their wallet, or pocket.

[^1]: A directed acyclic graph (DAG) is a directed graph with no directed cycles. That is, it consists of vertices and edges, with each edge directed from one vertex to another, such that following those directions will never form a closed loop.

In simpler terms, think of a DAG as a way to visualize and organize information that has a specific flow. Imagine a bunch of points, called vertices or nodes, connected by arrows (called edges). It is directed in that the arrows only go one way, showing a relationship between the points. It is acyclic in that you can't follow the arrows in a loop and end up back where you started. It's a one-way flow chart with no circular paths. This is useful for representing things that have a clear order or dependency.
