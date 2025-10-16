# Solidity

In 2014, the then CTO of Ethereum, Gavin Wood proposed Solidity as a Turing-complete language for writing smart contracts on Ethereum. The first public preview was unveiled at *Devcon0* in 2015. From then on, Solidity has undergone continuous development and a rapid release cadence. It quickly became the dominant language for Ethereum and other EVM-based blockchains. 

Solidity is statically typed language for writing smart contracts that compile to EVM bytecode before being executed by the consensus nodes. It follows the account-based model in which accounts are uniquely identified by an address.

Solidity’s rapid adoption was largely due to its friendly and familiar look and feel, which mirrored the experience found in other popular languages. C++, Python, and JavaScript were major influences on Solidity, so most developers find the learning curve smooth.

That said, it has its quirks too. Transactions are signed by a single user account and can trigger contract calls, transferring ETH from the caller account to the contract. The called contract can then call other contracts and cause a cascade. Transactions can also deploy new contracts, and this same contract code can be deployed multiple times. Control structures can include unbounded loops and recursion but are restricted to some extent by the gas-fee mechanism.

These features make Ethereum smart contracts powerful and user-friendly but also increase the attack vector and chance of them being manipulated by an adversary. These vulnerabilities are often not apparent until it is too late and something malicious has already occurred.

Gas fees are transaction fees paid in ETH to compensate for the computational resources used to process transactions and execute smart contracts. Every operation has a defined gas cost. The gas price is the amount of ETH (measured in gwei) you are willing to pay per unit of gas. The gas limit is the maximum amount of gas you are willing to spend on a transaction. 

This prevents runaway transactions that consume excessive resources. But there are variables affecting this process. Higher network activity leads to increased competition for block space and drives up gas prices. Complex transactions with more computational steps require more gas and results in higher fees. The gas price is dynamic and fluctuates based on supply and demand. Users can choose to pay a higher gas price to prioritize their transaction.

Gas fees are paid to the validators who secure the Ethereum network. These validators stake their ETH to participate in the consensus mechanism and earn rewards, including gas fees, for validating transactions and adding them to blocks.

This proof-of-stake system is not the one you may be used to on Cardano. Liquid staking isn’t native on Ethereum, and there are penalties like slashing in effect: you can lose some, or all, of your staked ETH.

**Question**

1. What is Solidity?
A)  A virtual machine for running smart contracts
**B) A programming language for writing Ethereum smart contracts**
C) A consensus algorithm used by Ethereum
D) A type of cryptocurrency wallet
