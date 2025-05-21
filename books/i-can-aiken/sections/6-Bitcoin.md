**Bitcoin (2008)**

Bitcoin's early days remain shrouded in mystery. In October 2008, a person (or group) using the pseudonym Satoshi Nakamoto published a whitepaper titled, *Bitcoin: A Peer-to-Peer Electronic Cash System*. It outlined a revolutionary system for decentralized digital currency, without the need for a domineering central authority. By late 2010, Satoshi withdrew from the Bitcoin community, leaving the project in the hands of its developers. 

Bitcoin's key tenets remain unchanged today:  

- **Decentralization**: Having no single entity in control makes Bitcoin censorship-resistant.
- A public ledger (the blockchain) records all transactions transparently–visible to everyone. 
- Having only 21 million Bitcoins in existence guarantees **digital scarcity**.
- Bitcoin has a multi-layered **security** system that features cryptographic hash functions, public-key cryptography and game theoretic[^1] incentives. These make it incredibly resilient against attacks. 
- Having no Turing-complete[^2] scripting language for smart contracts stymies expressiveness but also reduces its potential attack surface. 

Bitcoin's UTxO model is a fundamental aspect of its design. It governs how transactions are structured and how ownership of Bitcoin is tracked. Transactions are made up of inputs and outputs. Inputs refer to previous unspent transaction outputs, while transactions create new unspent outputs.

Rather than maintaining account balances, Bitcoin tracks individual unspent outputs. Each UTxO represents a specific amount of Bitcoin that can be spent in a future transaction. UTxOs can hold any nominal value, so, for example, it can be 1 BTC, 1694 BTC, or 0.000322 BTC. 

**Figure 5:** Bitcoin UTxO model 

To spend Bitcoin, a user’s wallet must reference specific UTxOs they own and provide a valid digital signature to prove ownership. This creates a chain of ownership in which each UTxO is linked to previous transactions, forming a transparent and traceable history.

Bitcoin's UTxO model is considered **stateless**. Unlike account based systems, the blockchain doesn't maintain a single global state. Instead, it keeps track of individual unspent transaction outputs. You can think of transactions as state transitions: Each consumes existing UTxOs and creates new ones. The set of all unspent UTxOs at any given time implicitly defines the state. We call this the **UTxO Set**.

Bitcoin’s UTxO model does not store account balances on the blockchain. Summing up the value of all UTxOs associated with its addresses calculates a wallet’s balance.

UTxO is stateless: each transaction is independent and doesn't rely on the previous state of any specific account. Transactions only need to verify the validity of the UTxOs being spent, not the overall state of the system. This enables parallel processing of transactions, as they don't conflict with each other as long as they are spending different UTxOs. 

[^1]: Reward Sharing Schemes for Stake Pools, iohk.io/en/research/library/papers/reward-sharing-schemes-for-stake-pools/
[^2]: In layman's terms, a Turing-complete system can execute any algorithm, or program, that any other computer or programming language can.
