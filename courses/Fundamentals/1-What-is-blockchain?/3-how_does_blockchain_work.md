**How does blockchain work?**

The term Distributed ledger technology (DLT) is often used interchangeably with blockchain. DLT is the infrastructure and protocols which enable simultaneous access, validation, and record keeping across a networked database. A Blockchain is just a specific type of DLT. 


Getting a little more technical, a blockchain is a chronological chain of linked, cryptographically secured blocks. Blockchains are ‘append only’, so you can only add data as part of a block. Each block  contains a list of transactions, a reference to the previous block and metadata about the transactions. It can also contain other things, but more about that later.

To understand how these blocks are chained together, we need to talk about **hashing**. 

Hashing is the process of using mathematical hash functions to take an input of data, which can be any size, and output a fixed size string. Hash functions are used throughout blockchain as you can use all sorts of input such as text, images, even videos of varying size and the output hash will always be a set length. The precise length of the output hash depends on which hashing algorithm you use. In blockchain systems, each block has its own hash that acts as a unique identifier. Each time a new block is created, its hash is produced based on the hash of the previous block. 

Blocks are connected through cryptographic hashes. Every block hash is unique as the odds of finding two different pieces of data which produce the identical hashes is practically impossible. Such a scenario where two separate inputs produce the same hash output is known as hash collision. This is basically why Blockchain is considered tamper proof as it is resistant to such hash collisions. 

Blockchains rely on a mix of cryptography and game theory to function correctly. In a blockchain context, game theory is about creating the right incentives so that enough rational actors will behave honestly otherwise their stake will be at risk. We’ll revisit these incentives later, for now, let's look at some of the other key cryptographic building blocks that feature in Blockchains.

**Public key cryptography** is where a user has a pair of keys, a private key they keep secret that is linked to a public key, which can be shared. The public key can be generated from the corresponding private key, but you can’t retrieve the private key from the public key. Therefore, there's no risk of compromise when sharing the public key, something the sender needs in order to send you something. Think of it like sharing your email address publicly, while you still keep your login password secret. Private key holders can also digitally sign a message with their private key. The receiver can then compare the public key with a signature and rest assured the message is from who it's supposed to be from.

Anyone who knows your private key can generate this signature to spend your funds, or reject a transaction, or otherwise impersonate you so it’s critical this key remains private. The different options to protect your credentials are covered in later courses.

Blockchains typically leverage a distributed **peer-to-peer** network for fault tolerance and transparency. The goal is for each peer to have the same blockchain data. If not, a peer can reach out to another peer for an update. Some networks are configured slightly differently. For example, Cardano’s network protocol only uses a ‘pull’ communication method for security reasons. If a node tries to ‘push’ information, it is automatically disconnected. Peer-to-peer networking ensures that a network outage impacting some of the peers won’t bring down everyone everywhere. The blockchain will continue to function, and when the disruption is resolved, the impacted peers can reach out to other peers and get updated with the latest blockchain data.

**Consensus mechanisms** are key to blockchains achieving immutability. A consensus mechanism is a protocol that brings all nodes of a distributed blockchain network into agreement (consensus) around a single data set. You can think of them as the verification standards through which each block gets added to the blockchain. 

There are various consensus mechanisms functioning on different blockchains today. They can be configured for certain requirements, with most having trade-offs around the blockchain trilemma. Proof of work and proof of stake are the two most common consensus mechanisms, and the focus of this course. The Cardano Blockchain Certified Associate, CBCA course goes into greater depth on alternative Proof of X mechanisms if you’re interested.

The real USP (unique selling point) of blockchain is that it guarantees integrity and trust in a distributed system even when participants are untrustworthy. In doing so, blockchain solves an old computer science problem referred to as the Byzantine general problem, which we’ll talk about next…
