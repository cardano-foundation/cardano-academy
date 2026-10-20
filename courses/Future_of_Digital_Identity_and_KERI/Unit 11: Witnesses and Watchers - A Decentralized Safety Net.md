# Witnesses and Watchers - A Decentralized Safety Net

## The Problem of "Two-Faced" Identity 

We have established that KERI gives you total control over your identity. But this power comes with a risk: If you control the history, what stops you from lying?

You could be telling Alice, "My key is X," but also telling Bob, "My key is Y"? This is called Duplicity, or being two-faced. In a centralized system, Google or a blockchain acts as the referee to stop this. But in KERI, there is no central referee. So, how do we catch a liar?

## The "Town Square" Model 

KERI solves this not by preventing you from lying, but by guaranteeing that if you lie, you will be caught immediately. It uses a decentralized safety net made of two roles: Witnesses and Watchers.

## 1. Witnesses (The Notaries) 

A Witness is a server that acts like a digital Notary or Town Crier.

Availability: You might turn your phone off, but your Witness stays online 24/7 to answer questions about your identity.
First-Seen Policy: Witnesses follow a strict rule: First Come, First Served. If you publish a Key Rotation event, the Witness stamps it and stores it. If you later try to change history and publish a different rotation for that same slot, the Witness rejects it.

## 2. Watchers (The Detectives) 

While Witnesses are helpful, they can be tricked or hacked. That is where Watchers come in. A Watcher is a passive observer, it could be your browser, your wallet, or a dedicated service…they can all take on this role.

Comparing Notes: Watchers listen to the Witnesses. They ask: "Hey Witness A, what is the latest event? Hey Witness B, do you agree?"
Duplicity Detection: If the Controller tries to cheat by sending one version of history to Witness A and a different version to Witness B, the Watcher notices the discrepancy instantly.

## Forging Consensus 

How do we know when to trust an event? We use a setting called TOAD (Threshold of Accountable Duplicity). This is simply a number. It defines how many Witnesses need to sign off on an event before it is considered "official."

Example: You designate five Witnesses and set your TOAD to 3.
The Rule: A validator, like a bank, will only accept your ID rotation if at least three of your fiveWitnesses have signed a receipt for it.
The Trap: If you act maliciously, you would need to compromise a majority of your Witnesses simultaneously. If you don't, the Watchers will spot the conflict, prove you are lying, and your identity effectively becomes worthless.

## Recap

Witnesses say: "I saw this event first." They are available 24/7 and operate on a “first seen” basis. Meanwhile Watchers say: "Do all the Witnesses agree?". They ensure Consistency and Fraud Detection. Together, they create a "safety net" that allows us to trust a decentralized identity without needing a blockchain. The system ensures that while you can try to lie, you cannot hide the evidence of your lie.

## Questions

1. What is “Duplicity” in the context of KERI’s Witnesses and Watchers? <br>
A. **Telling different parties conflicting versions of your identity history**<br>
B. Creating an identical backup of your identity<br>
C. Using two different wallets simultaneously<br>
D. Having two Witnesses confirm the same event<br>

2. What is the primary role of a Witness in KERI?<br>
A. To control the user’s private keys<br>
B. To issue new credentials on behalf of the user<br>
C. **To stay online, store a copy of the KEL, and follow a first-seen policy**<br>
D. To mine blocks on the blockchain<br>

3. What does TOAD stand for?<br>
A. Total Outstanding Authentication Devices<br>
B. **Threshold of Accountable Duplicity**<br>
C. Trusted Online Authority Database<br>
D. Temporary Offline Access Designation<br>

4. How does a Watcher detect fraud?<br>
A. By monitoring the user’s internet browsing history<br>
B. By scanning the blockchain for suspicious transactions<br>
C. By requiring the user to re-enter their password every hour<br>
D. **By comparing notes across Witnesses to find conflicting event histories**<br>

5. If your TOAD is set to 3 and you have 5 Witnesses, what must happen for an event to be accepted?<br>
A. All 5 Witnesses must sign a receipt<br>
B. **At least 3 of the 5 Witnesses must sign a receipt**<br>
C. Only 1 Witness needs to sign, and 3 must verify<br>
D. The event is automatically accepted without any Witness signatures<br>
