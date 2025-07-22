**Proof of stake**

Inevitably, alternative consensus mechanisms began to emerge exploring ways to address shortcomings with proof of work . One such alternative was the proof-of-stake consensus algorithm which was first muted on the Bitcointalk forum in 2011. Although both achieve consensus on blockchain, the means by which they get there is quite different. There are also different implementations of proof of stake, more about that later.

How does proof of stake (PoS) work? Proof-of-stake algorithms use a random election method to select a node that will be the validator of the next block. Who is chosen is based on a combination of criteria that can vary by blockchain, but generally include staking duration, amount of stake, randomization and node strength. 

A ‘validator’ is a generic term but think of it as the entity responsible for validating the next block on the chain. On Bitcoin, this is the miner, or mining pool. On Ethereum, it is the stake pool that is the validator. Also, note that with proof of stake, blocks are said to be ‘forged’, not mined.

The proof-of-stake system usually uses transaction fees as a reward, although additional incentives can be offered. Users participating in the "forging" process must **commit** a set amount of coins in the network. This represents their stake. Stake size determines the chances of a node being selected as the validator to forge the next block - the bigger the stake, the greater the chances. A little like a lottery, the more tickets you have, the greater your chances of holding the winning ticket.

Different methods are used to ensure a random selection process such as the ‘Randomized Block Selection’ and ‘Coin Age Selection’. With random block selection, validators are chosen based on nodes having a combination of lowest hash value along with highest stake. Whereas with Coin age selection, nodes are selected based on how long their tokens have been held. This is calculated by multiplying the number of days the coins are held by the number of coins. 

Once a node has forged a block, the age of its coins is reset to zero and the node must wait a set period of time before it is eligible to forge another block. This prevents a user with a large amount of coins (stake) from having too much control. Each blockchain  implements proof of stake differently with its own custom rules and configuration. For example, Algorand and Cardano rely on the Verifiable Random Function, one of cryptography’s most important discoveries dating back to 1999. 

When you stake ETH, you are essentially supporting a validator for the network. Randomly selected validators who hold a minimum amount of ETH are responsible for verifying transactions and adding new blocks to the blockchain. Validators, and their stakers, earn rewards through freshly minted ETH and network transaction fees.  

The stake serves as financial incentive for the forging node to behave honestly, as they have ‘something at stake’. If a forging node acts fraudulently, they may lose part, or all, of their stake and also the right to participate as a forger in future. A 51% attack works similar to what we described with proof of work, except, this time a bad actor would require a majority stake (51%) on the network. This is highly unlikely unless the value of the cryptocurrency is very low. 

The pros for proof of stake are energy efficiency and security. It is more inclusive as, usually, running a node is easy and affordable. High participation, along with the randomization process,  makes the network more decentralized as mining pools are no longer needed to mine blocks. It's important to note all proof-of-stake blockchains are not created equally. For example, some things to consider before staking on Ethereum:

- In September 2022, the Ethereum ‘Merge’ transitioned the blockchain from proof of work to proof of stake. This is only a step on a long Ethereum 2.0 roadmap. 
- you require a deposit of 32 ETH to run a staking node on Ethereum
- there is a lockup (bonding) period where your funds are not accessible. 
- Ethereum employs ‘slashing’ which is a penalty designed to deter dishonest validator behaviour. Slashing may result in the loss of a validator's staked ETH, and even removal from the network.

**Delegated proof of stake (DPoS)** is a consensus algorithm which extends the proof-of-stake idea. It was developed originally by Daniel Larimer in 2014. Holders of coins delegate to a validator, a little like voting for your chosen politician. You are effectively delegating staking responsibility to the validator. This is considered more efficient as many users will not have technical ability or time to run a validator. It is also democratic as the barrier to entry is low, and can be a one-time delegation. Otherwise, a lot of the functionality is similar to proof of stake. We’ll talk more about Cardano being the first provably secure proof-of-stake protocol, years before Ethereum transitioned.
