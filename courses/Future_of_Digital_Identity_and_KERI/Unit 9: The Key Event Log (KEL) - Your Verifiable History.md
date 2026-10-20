# The Key Event Log (KEL) - Your Verifiable History

## The Digital Logbook 

Think of the Key Event Log (KEL) as the ship's logbook for your digital identity. In most identity systems, the “truth” lives in a central database. Even with blockchains, your identity verification still depends on connecting to the network. 

KERI changes this by putting the truth in a file that you control. The KEL is a cryptographically secured, chronological diary of your identity's life. It records every time you created keys, changed them, or revoked them.

## Why "Autonomic"? 

We call this an Autonomic (self-governing) system.

Administrative Trust: Trusting a person (e.g., a bank manager).
Algorithmic Trust: Trusting a network (e.g., Bitcoin miners).
Autonomic Trust: Trusting the maths in your own history. With a KEL, you don't need to ask a blockchain "Is this ID valid?" You simply check the log. If the cryptographic signatures in the log connect perfectly from start to finish, the ID is valid.

## Deconstructing the KEL: A "Blockchain of One" 

Structurally, a KEL looks like a personal micro-blockchain. It is a chain of events where every link is locked to the previous one.

The core components are:

Key Events: The actual entry. "I am rotating my keys from Key A to Key B."
The Hash Chain: Each event contains a digital fingerprint, a Self-Addressing Identifier, of the previous event. This creates an unbreakable sequence. You cannot insert, delete, or reorder pages in this diary without breaking the chain.
Signatures: Every event is signed by your keys. This proves you authorized the entry.

## Types of Events 

Not all events are equal. We generally split them into two categories:
Establishment Events (Housekeeping): These are events that change the "control" of the ID—specifically Inception (creation) and Rotation (changing keys). These are critical because they determine who can sign for the ID.
Non-Establishment Events (Business): These are interaction events. You use these to sign data, anchor credentials, or interact with others without changing your keys.

## Security Superpowers 

Because the KEL is a self-contained history, it gives us security properties that centralized systems can't match:

### 1. Ambient Verifiability (Verify Anywhere) 

Because the KEL is just a file, it is portable. You can verify a KERI identity over Bluetooth, offline in a submarine, or across a local Wi-Fi mesh. You don't need to connect to a "universal resolver" or a blockchain node. If you have the KEL, you have the proof.

### 2. Evident Duplicity (Fraud Detection) 

In KERI, "Duplicity" means trying to keep two different versions of history—like a corrupt accountant keeping two sets of books. KERI doesn't strictly prevent you from trying this. Instead, it ensures that if you do try it, you are instantly caught. If you sign one event for Alice and a conflicting event for Bob, the moment those logs meet, the fraud is mathematically undeniable. This "burned bridge" destroys the trust in the ID forever.

## The KEL in the Ecosystem 

The KEL is the anchor for everything else in KERI:

- Witnesses: These are servers that store a copy of your KEL to ensure it's always available, even if your phone is off.
- TELs (Transaction Event Logs): While the KEL tracks your Identity, the TEL tracks your Data. For example, if you issue a driver's license, the status of that license (Active/Revoked) lives in a TEL, which is anchored to your KEL.

## Recap 

The Key Event Log is the "source of truth" for your identity. It replaces the need for a central registry with a verifiable, portable history file. But a log is only useful if we can secure the keys that sign it. In the next unit, we will explore KERI's most revolutionary security feature: Pre-Rotation, a way to protect your identity even if your private keys are stolen by a quantum computer.

## Questions

1. The KEL is best described as which of the following?<br>
A. A centralised cloud database for storing credentials<br>
B. A social media profile page<br>
C. **A cryptographically secured, chronological diary of your identity’s life**<br>
D. A blockchain smart contract<br>

2. What are “Establishment Events” in a KEL?<br>
A. Events that record business transactions<br>
B. **Events that change control of the ID, specifically Inception and Rotation** <br>
C. Events that delete old identity records<br>
D. Events that connect two users for the first time<br>

3. What does “Ambient Verifiability” mean?<br>
A. **A KERI identity can be verified anywhere, even offline, because the KEL is a portable file**<br>
B. Verification only works in specific data centres<br>
C. Verification requires a constant internet connection<br>
D. Only the identity owner can perform verification<br>

4. What is “Duplicity” in the context of KERI?<br>
A. Creating a backup copy of your KEL for safety<br>
B. **Trying to maintain two different versions of your identity history**<br>
C. Using the same key on two different devices<br>
D. Sharing your credentials with a trusted colleague<br>

5. What is the purpose of a Transaction Event Log (TEL)?<br>
A. It tracks cryptocurrency trades<br>
B. It records all internet browsing activity<br>
C. **It tracks data status (e.g., active/revoked credentials) and is anchored to the KEL**<br>
D. It stores backup copies of all signed documents<br>
