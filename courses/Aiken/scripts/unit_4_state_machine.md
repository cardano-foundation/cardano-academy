# State Machine

So the blockchain is essentially a state machine whose state updates as new blocks, full of transactions, are added. The scripting layer is where transactions are executed before they are bundled into blocks. 

For cryptocurrency to be useful, we need to be able to transfer value. This transfer is done via a transaction, usually after some conditions defined in a smart contract are satisfied. 

Each smart contract language works hand in glove with an accounting model which keeps a record of who owns what.

The two main accounting models are UTxO (Unspent Transaction Outputs) models and account-based models. 

While both models achieve a similar goal, they operate very differently. UTxO was introduced by Bitcoin, and the account-based model was subsequently introduced by Ethereum, then adopted by other mainstream blockchains such as Solana, Aptos, and Algorand. Cardano later extended the UTxO model, creating the extended UTxO model (eUTxO). 

You may be wondering why we didn’t mention the account model in the Cardano stack above. Which layer does it reside in? 

Before we give you our answer, understand that there is always some ambiguity about precise mappings to a suggested stack. Some models and protocols traverse, or impact, multiple layers. That said, if we were to place it, it would live somewhere between the settlement and consensus layers. eUTxO defines how the ledger state is represented and updated. It dictates how transactions are structured, validated, and how assets are owned and transferred. This is fundamental to the ledger's functionality. The eUTxO model also plays a crucial role in Cardano's consensus mechanism, Ouroboros. It enables efficient validation of transactions and ensures the integrity of the blockchain by preventing double-spending and other invalid state transitions.

Cardano’s eUTxO model, as the name suggests, extends the capability of UTxO but also takes learnings from the account model. As we move through the course, you will gradually begin to see how everything is related and that all the pieces matter.

Let’s take a step back in time to review each model and look at how each blockchain came to pass. Crypto’s origins stretch way back to the 1980s but we’ll begin our journey in 2008.

**Timeline**

1983 - Blind signatures (David Chaum)
1990 - eCash (digicash)
1991 - Haber & Stornetta describe cryptographically secured chain of blocks
1994 - Nick Szabo coins the idea of smart contracts. 
1999 - B-Money (Wei Dai)
2004 - Ripplepay
2004 - RPOS (Finney)
2005 - Bit Gold (Szabo)
2008 - Bitcoin (Satoshi Nakamoto)
2011 - Litecoin (Lee)
2012 - Ripple (McCaleb, Larsen)
2012 - Bitcoin Script brings basic smart contract capabilities to Bitcoin
2012 - Peercoin, 1st functioning proof-of-stake cryptocurrency
2013 - Ethereum whitepaper (Vitalik Buterin)
2013 - NXT features built-in smart contract templates
2015 - Ethereum genesis block is mined. 
2015 - Solidity, (Buterin et al.)
2015 - IOHK (now IOG) is founded by Charles Hoskinson & Jeremy Wood. 
2015 - Early development on Cardano begins
2016 - Ethereum DAO bug exploited resulting in hard fork 
2016 - Hyperledger Fabric is launched
2017 - EOS blockchain introduces smart contracts written in C++
2017 - Cardano is launched with the Byron bootstrap era
2017 - Bitcoin Cash created through a hard fork
2018 - IOHK releases the Plutus Platform at PlutusFest
2020 - Cardano Shelley era transitions from a federated to fully decentralized network. Staking rewards are introduced 
2020 - Cardano Goguen era begins with Mary hard fork enabling native token support 
2021 - Cardano Alonzo hard fork introduces smart contract support
2022 - Cardano Vasil hard fork introduces Plutus V2 
2022 - Ethereum transitions from proof-of-work to proof-of-stake 
2023 - Aiken co-founder Lucas Rosa authors Cardano Foundation blog post introducing Aiken 
2024 - Cardano Chang hard fork brings on-chain governance & Plutus V3 
2024 - Aiken GA release announced on X
2025 - Plomin hard fork

**Questions**

1.  Which accounting model was introduced by Bitcoin?
A. **UTxO (Unspent Transaction Outputs)**
B. Account-based model
C. Extended UTxO (eUTxO)
D. Hybrid model

2. Which of the following was the first phase of Cardano?
A. Shelley (decentralization)
B. **Byron (bootstrap phase)**
C. Voltaire (governance)
D. Goguen (smart contracts)

3. What is the primary purpose of an accounting model in a blockchain system?
A. To execute smart contracts
B. To facilitate communication between nodes
C. **To track ownership and transfer of assets**
D. To ensure the security of the blockchain

4. Which accounting model was initially introduced by Ethereum?
A. UTxO (Unspent Transaction Outputs)
B. **Account-based model**
C. Extended UTxO (eUTxO)
D. Hybrid model


