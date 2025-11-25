# Handlers
So we have extended the UTxO model to enable arbitrary transactional logic to place conditions on who can consume a UTxO. But we never talked about what the purpose of all this is? Cardano’s eUTxO model allows six specific purposes that describe the goal of a validator.

## Spend

A validator with a spend purpose uses either a public key address or a script address to validate the spending of a UTxO. The script whose hash matches the script address must be included in a transaction intending to spend the UTxO at that script address. This script is executed during validation. 

The script is validated based on the datum attached to the unspent UTxO, the redeemer and the transaction itself. Note the datum is only provided with a spend purpose, and even then it’s optional.

## Withdraw

The withdraw purpose is about withdrawing staking rewards. We said a UTxO's address can be a public key address or a script address, and either can optionally include a staking credential. A UTxO can hold ada, which can be spent or delegated to an SPO to secure the network and also earn staking rewards. 

Like before, a staking credential can also contain a public key hash or a script hash. Also like before, to be eligible to withdraw rewards from the reward account associated with a staking credential containing a script hash, the script with that particular hash must be included in the transaction. This script is executed during validation.

## Publish

A script with a publish purpose controls how to publish delegation certificates. You need to publish certificates in a transaction for a number of reasons:

- To register a staking credential in order to create a rewards account tied to your staking credential
- De-registering a credential and rewards account 
- Delegating a staking credential, and ada at your address, to a stake pool 

Again, like before, if the staking credential contains a script hash, the transaction must include the script with that hash, and this script is executed during validation. This does not apply to registering.

For large stake pools, you might use such a script to check that a minimum number signatures are present for an important action, like de-registering or changing the SPO to whom you are delegated to.

## Mint

Scripts, or validators, with the mint purpose validate whether native assets can be minted or burned. The rules that dictate the creation or destruction of an asset are defined by its minting policy. Each native asset on Cardano is uniquely identified by its CurrencySymbol and TokenName. A transaction attempting to mint new assets for a given CurrencySymbol must include the script whose hash matches the CurrencySymbol. This is the script executed during validation.

## Vote

A script with the vote purpose is used in governance to validate votes from either a delegate representative, DRep, or a constitutional committee member, CCM. If one or more votes tied to a script hash are included in a transaction, the script with that hash must be included and executed to validate the vote.

## Propose

Finally a script with the propose purpose is the least used but most important script. It is also known as a constitution script or guardrail script, as it prevents spammy proposals from flooding the network. For example, a proposal that would treble the supply of ada couldn’t even be submitted. In other words, a validator with a propose purpose is the codified enforcement of the constitution.  It validates two kinds of governance actions: ParameterChange and TreasuryWithdrawals.

## Questions

1. Which of the following is NOT a valid purpose for a script in the Cardano eUTxO model?

A) Mint
**B) Revoke** 
C) Vote
D) Withdraw

2. What is a minting policy in the context of Cardano native assets?

A) A government regulation that controls the issuance of new tokens
B) A community-driven process for deciding on new token features
**C) A script that defines the rules for creating and managing a native asset**
D) A smart contract that automatically distributes tokens to users
