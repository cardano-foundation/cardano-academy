# KERI - A New Foundation for Trust

## The Quest for a Universal Trust Layer 

We have established that the internet lacks a native identity layer. To date, we have tried to patch this flaw with two main models, but both have failed to scale globally.

## 1. The Administrative Trust Basis (The "Doorman")

Used by DNS and Certificate Authorities, this relies on a trusted third party to issue IDs.

The flaw is that it’s fragile. If the Administrator is hacked, which happens frequently, the integrity of every ID they issued is compromised.

## 2. The Algorithmic Trust Basis (The "Blockchain") 

Used by most Decentralized Identifiers (DIDs), this relies on a distributed ledger.

The limitation for identity specifically is that it ties your ID to one ledger's ecosystem:
* Portability Constraints: Your ID is anchored to a specific ledger. Moving between chains requires bridges or wrappers.
* Cost Inheritance: Your identity inherits the fee structure of whichever chain it lives on — fine for high-value transactions, less practical for everyday identity checks.
* The Interoperability Challenge: With 200+ DID methods, the community built "Universal Resolvers" to bridge them — but this adds architectural complexity that KERI can avoid."

## The KERI Solution: Autonomic Trust 

KERI introduces a third paradigm: Autonomic Trust. Instead of trusting an administrator or a blockchain, you trust the Identifier itself. This is possible because the Identifier is Self-Certifying.

## How an Autonomic Identifier (AID) Works 

In KERI, we don't look up an ID in a registry to find the owner. The ID is the owner's cryptographic fingerprint.

* The Maths: The Identifier is generated directly from your Public Key (or a mathematical digest of it).
* The Result: You don't need a third party to verify who controls the ID. The maths proves that only the person holding the corresponding Private Key could have created it. This makes the ID Portable, in that it works anywhere, and Secure… no one can delete it.

## The Pillars of KERI 

To make this work securely at internet scale, KERI relies on three mechanisms:

## 1. The Key Event Log (KEL) 

The KEL is the "Single Source of Truth." It is a personal, tamper-proof diary of your identity. It is an append-only chain of events. Each new event, like rotating a key, includes a hash of the previous event. This creates an unbreakable chain—you cannot change your history without breaking the cryptographic links.

## 2. Pre-Rotation (The Security Engine) 

In traditional systems, if a hacker steals your key, they can lock you out. KERI solves this by separating Active Keys (used for signing) from Rotation Keys (used for recovery).

* The Mechanism: When you create an ID, you cryptographically commit to your next key (Pre-Rotation), but you keep that key hidden offline.
* The Benefit: Even if a hacker steals your active key, they cannot rotate it, because they don't have the hidden Rotation Key. This provides Post-Quantum Security and ensures you can always recover your identity.

## 3. Witnesses and Watchers (The Safety Net) 

How do we ensure a user doesn't lie about their history? We use a network of Witnesses.

* Ambient Verifiability: Witnesses are servers that store a copy of your KEL. They don't control your ID; they just confirm when events happened.
* Duplicity Detection: If a malicious user tries to rewrite history (Duplicity), the Witnesses and Watchers detect the conflict immediately. The fraud becomes mathematically provable, destroying the trust in that ID forever.

## Recap

KERI isn't just another DID method. It is a fundamental rethink of digital trust. It acts as a "Trust Spanning Layer"—a narrow waist that connects any application to any infrastructure.

* KERI handles the Identity.
* ACDC handles the Data.
* CESR, which stands for Composable Event Streaming Representation, handles the Encoding…we’ll talk about both of these shortly.

## Questions

1. In KERI, what does “Self-Certifying” mean?<br>
A. The identifier is verified by a central registry<br>
B. The identifier is generated from your public key and proves ownership through maths<br>
C. The identifier is issued by a government agency<br>
D. The identifier must be renewed every year<br>

2. What is the Key Event Log (KEL)?<br>
A. A personal, tamper-proof, append-only chain of identity events<br>
B. A blockchain that records all global transactions<br>
C. A cloud database controlled by a Certificate Authority<br>
D. A backup copy of your email inbox<br>

3. What happens when Witnesses and Watchers detect duplicity?<br>
A. The user’s identity is automatically renewed<br>
B. The fraud is ignored until a manual review<br>
C. The fraud becomes mathematically provable, destroying trust in that ID<br>
D. The user is given a warning and a second chance<br>

4. How does Pre-Rotation protect against key theft?<br>
A. It encrypts the active key with a stronger algorithm<br>
B. It stores a backup key with a trusted third party<br>
C. It prevents anyone from ever changing their keys<br>
D. It separates active signing keys from hidden rotation keys kept offline<br>

5. KERI is described as a “Trust Spanning Layer.” What does this mean?<br>
A. It connects any application to any infrastructure for identity verification<br>
B. It only works on a single blockchain<br>
C. It replaces all existing internet protocols<br>
D. It requires a VPN connection to function<br>
