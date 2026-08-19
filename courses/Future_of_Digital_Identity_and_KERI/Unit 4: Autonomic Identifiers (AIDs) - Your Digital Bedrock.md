# KERI - A New Foundation for Trust

## The Quest for a Better ID 

We have established that the internet lacks a native trust layer. To date, we have relied on two flawed models:

* Administrative Trust: Trusting a central authority (like a Certificate Authority) to issue IDs. Flaw: Single point of failure.
* Algorithmic Trust: Anchoring IDs to a blockchain. Limitation for identity: ties your identifier's lifecycle to a single network's performance characteristics and fee model.

These limitations highlight the urgent need for a new foundation. We need an identifier that doesn't rely on a "Middleman" or a "Network." We need The Autonomic Identifier (AID).

What is an AID? Think of an AID as Digital DNA. In traditional systems, your ID is just a random number assigned to you by a database (like a Row ID). In KERI, your ID is Cryptographically Derived. It is generated directly from your Public Key.

* Self-Managing: You create it yourself. You don't ask permission.
* Self-Certifying: You don't need a registry to prove it's yours. The maths proves that only the person holding the private keys could have created this specific ID.
* Portable: Because the proof is in the ID itself, you can use it anywhere—on any blockchain, any network, or even offline.

## The Three Pillars of AID Security 

How do we make this secure without a central bank or blockchain? We rely on three pillars:

## 1. The Key Event Log (KEL) 

The KEL is the Diary of your identity. It is a tamper-proof chain of events. Every time you change your keys or settings, it is recorded here. Each event is cryptographically linked to the previous one, creating an unbreakable chain of history.

## 2. Self-Certification 

This is the cryptography element. Because the ID is derived from the "Inception Key" (the key used to create it), the binding is mathematical, not administrative. You verify the ID by checking the signature, not by calling a helpdesk.

## 3. Pre-Rotation (The Insurance Policy) 

This is the Game Changer. In most systems (like Bitcoin), if someone steals your private key, they own your assets forever. KERI solves this with Pre-Rotation.

* The Mechanism: When you create your ID, you cryptographically commit to your next key (Pre-Rotation), but you keep that key hidden offline.
* The Benefit: If your active key is stolen, the thief cannot lock you out, because they don't have the hidden "Rotation Key." You use the hidden key to revoke the stolen one and regain control.

## The Power of AIDs in Practice 

This architecture translates into massive real-world advantages:

## 1. True Portability 

AIDs are not "Ethereum DIDs" or "Hyperledger DIDs." They are universal. KERI acts as a "Trust Spanning Layer," allowing your identity to move freely between different networks and platforms.

## 2. Flexible Hierarchy (Chain of Command) 

AIDs are designed for organizations, not just individuals. They support Delegation.

* A Root Organization, e.g., the Global Legal Entity Identifier Foundation, GLEIF, can delegate to an Issuer.
* The Issuer can delegate to a Company.
* The Company can delegate to a CEO. This creates a verifiable chain of trust that mirrors how real businesses operate (like the vLEI ecosystem).

## 3. Unprecedented Recovery 

With the combination of Pre-Rotation and a "Watcher Network" (observers who check for fraud), you can detect a hack instantly and recover your identity before damage is done. This level of safety is unique to KERI.

## Recap 

The Autonomic Identifier (AID) is the solution to the "Internet's Missing Layer." By replacing brittle Administrative models and heavy Algorithmic models with a Cryptographic Foundation, we get an identity that is:

* Secure (Quantum-resistant via Pre-Rotation).
* Portable (Works everywhere).
* Verifiable (Trust the maths, not the middleman).

This is the bedrock of the Veridian platform, which we will introduce in the next unit.

## Questions

1. How is an Autonomic Identifier (AID) generated?<br>
A. **Cryptographically derived from the user’s public key**<br>
B. Randomly assigned by a central database<br>
C. Issued by a blockchain mining node<br>
D. Created by a Certificate Authority on request<br>

2. What makes an AID “Portable”?<br>
A. It can only be used on mobile devices<br>
B. **The proof is contained in the ID itself, so it works on any network or offline**<br>
C. It is stored on a USB stick that can be carried anywhere<br>
D. It requires an internet connection to function on any platform<br>

3. In the vLEI ecosystem, what does the delegation chain look like?<br>
A. CEO → Company → Issuer → GLEIF<br>
B. Company → GLEIF → CEO → Issuer<br>
C. **GLEIF → Issuer → Company → CEO**<br>
D. Issuer → CEO → GLEIF → Company<br>

4. What is the “Inception Key” in KERI?<br>
A. A backup key stored in a government vault<br>
B. **The key used to create the identifier, forming the mathematical binding**<br>
C. A temporary key that expires after 30 days<br>
D. A universal master key shared among all KERI users<br>

5. Why is Pre-Rotation described as an “insurance policy”?<br>
A. It guarantees financial compensation for identity theft<br>
B.  It provides free legal representation in court<br>
C. It backs up your identity to a government server<br>
D. **It ensures you can recover your identity even if your active key is stolen**<br>
