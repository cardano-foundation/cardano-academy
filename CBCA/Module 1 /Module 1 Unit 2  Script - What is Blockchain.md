# Unit 2 - What is Blockchain

## Learning Objectives
By the end of this unit, the learner should be able to:

- Give a high-level definition of what blockchain is
- Understand the main components of a typical blockchain network 
- Understand a simple blockchain data structure
- Learn the use cases of blockchain technology and how it helps different industries 
- Learn about career opportunities in blockchain

## Introduction
Hello everyone, and welcome. I am your lecturer, [lecturer name]. In this unit, we will look into how blockchain works at a basic level. Follow along at your own pace. Feel free to go back and review as needed.

## Table of Contents
Previously, we talked about consensus algorithms. These help distributed networks reach agreement without a central authority. Now we will learn about blockchain and who participates in it. We’ll also touch on some use cases. We have plenty to cover, so let’s get started!

## The First Message from Satoshi
In 2008, Satoshi Nakamoto introduced blockchain technology. The publication of the Bitcoin whitepaper describing a peer-to-peer electronic cash system kicked off a whole new era of blockchain technology and digital currencies. The key innovation was a new mechanism allowing users in a network to reach agreement on various decisions without a central manager or controlling entity. The way the agreement is reached is called a consensus algorithm. Bitcoin introduced the proof-of-work consensus algorithm. 

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.1.png)

Satoshi wasn’t the first to propose a digital currency by any means. In 1998, Nick Szabo proposed Bit Gold, but it was never implemented. Bitcoin was – in 2009. It became the first successful attempt to create a decentralized digital currency. It’s widely considered a true financial innovation.

Others quickly started building on the ideas introduced by Bitcoin. Blockchain technology provides an opportunity to decentralize many applications across industries like insurance, banking, logistics, supply chain management, agriculture, and more.

Some still associate blockchain with Bitcoin, but blockchain technology isn’t Bitcoin, and there have been many successful innovations, like Cardano and Ethereum.

## Main Components of a Blockchain

What exactly is a blockchain? It allows users to send and receive digital assets securely and transparently without needing a central authority or intermediary. It achieves this by having a copy of all transactions, or ledger, duplicated and distributed across a network of computer nodes. These nodes work to reach agreement, and keep in sync using a consensus mechanism. This set of interconnected nodes stores data or items of value in blocks, where each block is tied to the previous, resulting in a chain of blocks. That’s how we get the name blockchain.

Blockchain technology, also referred to as Distributed Ledger Technology, or DLT, provides a decentralized and accessible data structure for conducting many kinds of transactions, ranging from financial payments to information exchange, from commerce to Internet of Things. [Ref.2.2].

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.2.png)

As shown on the diagram, blockchain technology consists of several components. It generally includes network nodes, a peer-to-peer network, a consensus algorithm, and a chain of blocks that form the decentralized ledger.  

In a blockchain network, nodes are users who submit transactions and block producers who create blocks for the chain. These transactions and blocks are transmitted through the peer-to-peer, or P2P, network.

A true P2P network has a distributed structure, meaning there is no central node. All nodes are equal, with no special privileges, and they communicate with each other to share and exchange information.

A consensus algorithm is necessary for the different block producers to reach agreement when creating a new block to add to the chain. The consensus algorithm used in the Bitcoin network is called proof of work. We’ll cover this in more detail in another unit. 

## Data Structure of a Blockchain
Let’s dive into the different components of a blockchain, starting with blocks. 
Blocks contain verified transactions linked to each other in a chain in chronological order. Transactions cannot be altered; they become permanently inscribed in the block. This is an important blockchain feature in that it stores records immutably, meaning they cannot be changed, forged, or even deleted, as this would break the chain of blocks.

Each block has a header and a body.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.5.png)

The block body contains transaction data. A transaction might be a financial payment sending a digital asset from one user to another, or a supply chain transaction of a product being shipped from one facility to another. Typically, a block contains multiple transactions.

The block header contains its time stamp and a hash–proof of everything contained in the block body as well as the hash of the previous block.  

## Hash Function
Let’s start with that hash in the block header. What is it?

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.3.png)

A hash function is used to obtain a compact representation of some piece of data – a block for example. It takes an input and returns a fixed-size output called a hash digest. It’s a one-way mathematical function. It can’t be reversed, meaning the original input can’t be derived from the hash. You can think of hashes as a way to ‘compress’ data.

Any changes to the original input will be reflected in a completely different hash output. We’ll explore hashing in greater depth in the following units. 

## How Are Blocks Chained Together
Let's go back to our earlier diagram of the blockchain structure and see how those blocks are chained together. Any ideas? 

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.5.png)

If your answer was ‘the hash of the previous block’, you’re correct. Every block in the blockchain contains the hash value of the previous block. This hash then becomes a part of the hash of the next block, which becomes a part of the next block, and so on. It is this hashing of hashes that chains the blocks together. 

If someone attempts to make a change to a block, its hash changes. Because that hash is in the next blocks, all subsequent blocks change too. If the hash changes, the network will reject the change. 

And with that, we’ve reached the first milestone in your blockchain journey: getting a high-level understanding of what blocks are and how they’re chained together. Congratulations. If you need to review any of the concepts covered, just pause the video, go back, and continue whenever you’re ready. 

**Shall we go on?**

## Use Cases
Let’s briefly discuss use cases.

Blockchain builds trust into network nodes through its consensus algorithm, empowering designers and innovators to rethink applications that no longer use a central authority.  Decentralized, distributed networks have the potential to change how we interact with existing societal organizations like banks, businesses, and the government.

There are use cases like enabling peer-to-peer currency transactions in finance, improving supply chain management and logistics tracking, managing identity, verifying and authenticating digital assets, and even facilitating eVoting and elections.

In finance, for instance, blockchain allows for true peer-to-peer currency to function without commercial banks involved. Removing intermediaries has profound implications for the future of money. The societal impact has the potential to change traditional power structures, leading to new forms of social and economic organization.

One organizational structure that can exist on a blockchain is called a DAO, or Decentralized Autonomous Organization. DAOs have the potential to change how we think of organizations like companies. And these are just a few examples of the numerous potential uses for blockchain.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.6.png)

## Careers in Blockchain
Blockchain technology has created, and will continue to create many jobs in the industry. Traditional roles in analysis, coding, economics and security can transfer to blockchain with upskilling. The titles may just change to smart contract developer, token economist, DeFi analyst, and so on. Technical and non-technical skills along with a burning curiosity can bring success in this rapidly evolving industry. 

Blockchain is also driving research and development in many areas of science from cryptography to compliance. There has been significant progress in consensus algorithms, multi-party computation, and programming languages, for example. 

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.7.png)

## Review
So here we are, at the end of this unit, covering the basics of blockchain.
We looked at a blockchain's main components, block creation, and block data. We looked at the importance of the hash mechanism, and how this effectively allows to create ‘a chain of blocks’. 

That’s it for now, and I will see you next time.

## Reference
[Ref.2.1] S. Nakamoto, “Bitcoin: A Peer-to-Peer Electronic Cash System”, 2008, Available: https://bitcoin.org/bitcoin.pdf, Accessed: 20 Aug 2022.<br>
[Ref.2.2] “What is a blockchain?”, Available: https://docs.cardano.org/new-to-cardano/what-is-a-blockchain, Accessed: 20 Aug 2022.<br>

## Questions

**Sub-Unit 1**

*Blockchains need consensus algorithms. In a blockchain, consensus algorithms:* 
- Force all participants to agree
- **Allow participants to reach a decision without a central authority (CORRECT ANSWER)**
- Allow participants to reach a decision with the help of a central authority
- Expel malicious or faulty participants

**In a typical blockchain:**
- Decisions are made by an elected leading authority
- Decisions are made at random.
- There’s no decision to be made
- **Decisions are reached through a consensus algorithm (CORRECT ANSWER)**

**Sub-Unit 2**

*Which of the following is not a fundamental component of blockchain technology?*
Network nodes
- A peer-to-peer network
- A consensus algorithm
- **A decentralized autonomous organization (CORRECT ANSWER)**
- A chain of blocks that form the distributed ledger

*Which of the following better describes blockchain technology?*
- Internet of things (IoT)
- Artificial intelligence (AI)
- **Distributed ledger technology (DLT) (CORRECT ANSWER)**
- Decentralized finance (DeFi)

*A blockchain allows users to send and receive digital assets securely and without needing a central authority or intermediary.*
- **TRUE (CORRECT ANSWER)**
- FALSE

*Examine the image below and select the correct labels. (Image Questions)*

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.8.png)

- A: Encryption Algorithm; B: Communicator; C: Network Nodes
- **A: Consensus Algorithm; B: Block Producer; C: Chain of Blocks (CORRECT ANSWER)**
- A: Block Producer; B: Encryption Algorithm; C: Chain of Blocks

**Sub-Unit 3**

*In blockchain, each block has a header and a body. Generally speaking, what’s part of the header?*
- Time stamp and transaction data
- Hash of previous block and transaction data
- **Hash of previous block and time stamp (CORRECT ANSWER)**
- Hash of previous block, time stamp, transaction data

*A block header contains complete transaction data.*
- TRUE 
- **FALSE (CORRECT ANSWER)**

**Sub-Unit 4**

*A hash function produces a fingerprint of data, creating an output for a given input. Select the correct one.*
- **A hash function creates a fixed-size output (CORRECT ANSWER)**
- The size of the output depends on the input
- Each system decides if the length of the output is fixed or not
- The size of the output is dynamic

*What maintains the integrity of a blockchain?*
- Each block has a unique, independent identifier
- Each block contains the next block's hash
- **Each block includes the previous block's hash (CORRECT ANSWER)**
- Each change in a block only impacts that block's hash

*Select the image that shows the correct data structure of a block. (Image Question)*
- Image 1:
![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.9.png)

Header, Time Stamp, Hash of next block, Transaction data, Body, Proof of Body
- Image 2:
![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.10.png)

Header, Hash of Previous Block, Proof of Header, Time Stamp, Body, Transaction Data
- Image 3: 
![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.2.11.png)
**Header, hash of previous block, time stamp, proof of body, Body, Transaction data (CORRECT ANSWER)**

*What links blocks together?*
- **The hash of the previous block (CORRECT ANSWER)**
- The date when the new block was created
- The time stamp of all blocks
- The transaction data ID

