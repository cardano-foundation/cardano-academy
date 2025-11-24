# Cardano Addresses

A Cardano address usually has 3 parts. We say usually because the delegation credentials are optional and sometimes the payment and delegation credentials are the same.
The first part is the header which describes the address type and which network it exists on–mainnet, testnet, etc.

## Payment Credentials

Every address has a payment credential. This determines under which conditions a UTxO residing at that address can be spent. If the payment credential is given by a payment pub key hash, the hash of a payment verification key, then each transaction that wishes to spend a UTxO at that address has to sign with the corresponding payment signing key. The payment credential of an address can also be the hash of a script, where this script is evaluated when validating a transaction trying to spend a UTxO at the address. In this case, the script effectively becomes the owner of the UTxO at the address.

Remember we said UTxOs are like vouchers. You can use them in transactions for services. And you can attach additional instructions to them, so a voucher could be a restaurant order that the waiter hands to the kitchen and shouts “order in!” The details of your order appear on your voucher. If the meal is served as ordered, the voucher is consumed as payment and new vouchers are created for the tip and the change back to you.

Just like you have to submit your order to the waiter, on Cardano you submit your transaction to the network node for validation. It validates the transaction using the address’s payment credentials, which come in one of two forms:

- a verification key hash digest;
- a script hash digest.

In the first form, the network node, or the waiter in our analogy, asks for your digital signature using the signing key that corresponds to the verification key. This mechanism, based on asymmetric cryptography, is simple and intuitive but doesn’t allow any means to express additional validation logic.

This is where Cardano’s eUTxO model extends UTxO by enabling locking of UTxO with a script that describes the arbitrary validation logic that must be satisfied for the funds at that address to be spent. This is why smart contracts on Cardano are often referred to as “validators,” which guard the UTxO. Such addresses are called script addresses. Similarly to before, the entire script has to be provided as a witness with any transaction spending from a script address. There can be multiple scripts in a transaction and all must return True for the transaction to be valid. 

## Delegation Credentials

The third part of the address is the delegation credentials. These optional credentials dictate what can be done with the staked ada sitting at this address. On Cardano, ada holders delegate their stake to stake pools run by stake pool operators, or SPOs. Delegating the stake associated with an output is counted by the protocol as if it belonged to the stake pool, and this increases their chance of being elected as the next block producer. To incentivise staking, the Cardano protocol distributes a share of the block-producing rewards to delegators. It’s important to note that it is the protocol itself which automatically distributes all rewards, and the stake is liquid, never locked or inaccessible.

To recap, the payment credentials control how to spend UTxOs, while delegation credentials control the following:
how to delegate stake to a stake pool by publishing a delegation certificate
how to withdraw rewards tied to the stake credentials
Just like with payment credentials, delegation credentials can take the form of a verification key hash digest or a script hash digest.

## Questions

1. What is a validator in the context of Cardano smart contracts?

A) A central authority that approves transactions
B) A hardware device used to store cryptographic keys
**C) A script that outlines the conditions for spending a UTxO**
D) A software program that executes on the Ethereum Virtual Machine

2. What is the purpose of delegation credentials in a Cardano address?

A) To control the minting and burning of native assets
B) To define the spending conditions for a UTxO
**C) To manage the delegation of ada to stake pools**
D) To specify the voting rights associated with an address

3. What is the main advantage of using scripts to lock UTxOs?

A) It reduces the size of transactions
B) It simplifies the validation process
**C) It enables arbitrary validation logic**
D) It increases the speed of transactions
