# Bitcoin UTxO

Bitcoin's early days remain shrouded in mystery. In October 2008, a person (or group) using the pseudonym Satoshi Nakamoto published a whitepaper titled, Bitcoin: A Peer-to-Peer Electronic Cash System. It outlined a revolutionary system for decentralized digital currency, without the need for a domineering central authority.  By late 2010, Satoshi withdrew from the Bitcoin community, leaving the project in the hands of its developers.


Bitcoin's key tenets remain unchanged today:  

- **Decentralization**: Having no single entity in control makes Bitcoin censorship-resistant.
- A public ledger (the blockchain) records all transactions transparently–visible to everyone. 
- Having only 21 million Bitcoins in existence guarantees digital scarcity.
- Bitcoin has a multi-layered security system that features cryptographic hash functions, public-key cryptography and game theoretic incentives. These make it incredibly resilient against attacks. 
- Having no Turing-complete scripting language for smart contracts stymies expressiveness but also reduces its potential attack surface. 

Bitcoin's UTxO model is a fundamental aspect of its design. It governs how transactions are structured and how ownership of Bitcoin is tracked. 

Transactions are made up of inputs and outputs. Inputs refer to previous unspent transaction outputs, while transactions create new unspent outputs.

Rather than maintaining account balances, Bitcoin tracks individual unspent outputs. Each UTxO represents a specific amount of Bitcoin that can be spent in a future transaction. UTxOs can hold any nominal value, so, for example, it can be 1 BTC, 1694 BTC, or 0.000322 BTC. 

To spend Bitcoin, a user’s wallet must reference specific UTxOs they own and provide a valid digital signature to prove ownership. This creates a chain of ownership in which each UTxO is linked to previous transactions, forming a transparent and traceable history.

Bitcoin's UTxO model is considered stateless. Unlike account based systems, the blockchain doesn't maintain a single global state. Instead, it keeps track of individual unspent transaction outputs. You can think of transactions as state transitions: Each consumes existing UTxOs and creates new ones. The set of all unspent UTxOs at any given time implicitly defines the state. We call this the UTxO set.

Bitcoin’s UTxO model does not store account balances on the blockchain. Summing up the value of all UTxOs associated with its addresses calculates a wallet’s balance.

UTxO is stateless: each transaction is independent and doesn't rely on the previous state of any specific account. Transactions only need to verify the validity of the UTxOs being spent, not the overall state of the system. This enables parallel processing of transactions, as they don't conflict with each other as long as they are spending different UTxOs. 

**Questions**

1. Who is credited with the creation of Bitcoin?
A) Vitalik Buterin
**B) Satoshi Nakamoto**
C) Gavin Wood
D) Charles Hoskinson

2. Which of the following is NOT a core principle of Bitcoin?
A) Decentralization
B) Transparency
**C) Turing-completeness**
D) Scarcity

3. What is the maximum number of Bitcoins that will ever exist?
A) 10 million
**B) 21 million**
C) 100 million
D) Unlimited

4. How are Bitcoin transactions structured?
A) Account balances
**B) Inputs and outputs**
C) Smart contracts
D) State transitions

5. Which statement best describes the UTxO model?
A) It maintains a global state of all account balances
**B) It tracks individual unspent transaction outputs**
C) It relies on a central authority to validate transactions
D) It is primarily used for complex smart contracts

6. How is a Bitcoin wallet's balance calculated?
A) By checking the balance stored in the blockchain
**B) By summing the value of all UTxOs associated with the wallet's addresses**
C) By querying a central server
D) By contacting the Bitcoin miners


7. What is a key characteristic of the UTxO model in terms of state?
**A) Stateless**
B) Stateful
C) Semi-stateful
D) Dynamic

