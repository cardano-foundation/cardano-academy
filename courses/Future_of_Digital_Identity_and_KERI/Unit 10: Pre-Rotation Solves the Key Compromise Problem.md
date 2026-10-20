# Pre-Rotation Solves the Key Compromise Problem

## The Achilles' Heel of Digital Identity 

In almost every digital identity system, even Bitcoin or any traditional Public Key Infrastructure (PKI), the private key is a single point of failure. If a hacker steals your private key, they become you. They can sign transactions, steal assets, and impersonate you perfectly.

Worse, they can lock you out. In traditional systems, if you want to rotate or change your keys, you need to sign the request with your current key. If the hacker has that key, they control the rotation. They can rotate the keys to their own device, effectively stealing your identity forever. So how do we solve this problem?

## Pre-Rotation 

KERI solves this with a feature called Pre-Rotation. It doesn't just make rotation harder; it changes the rules of the game. The core concept is simple: Don't use the same key for "Signing" and "Rotating."

Think of the signing keys as hot. These are on your phone or laptop. You use them daily. If they are stolen, it’s annoying, but not fatal. Your rotation keys are Cold. These are generated in advance but kept offline, for example, on a piece of paper or an air-gapped USB. You only use them once: to recover your account.

## How It Works 

To understand Pre-Rotation, imagine a sealed envelope.

1. **Inception**, sometimes called the Commitment, is when you create your identity. You generate Key Set A for today and Key Set B for tomorrow.
- You **publish** Key Set A so people can verify your signatures.
- You **hide** Key Set B. You hash it, take a digital fingerprint, and publish only that hash. This is like showing the world a sealed envelope and saying, "My next key is inside."
2. **An attack** occurs and a hacker steals Key Set A. They try to rotate the keys to take control. But the network asks: "Prove you have the key in the envelope." The hacker can't, because they only have the hash, the envelope, but not the key inside.
3. **Recovery**, or the Reveal: You go to your safe, get Key Set B, and publish a rotation event. The network checks: "Does this key match the envelope you showed us earlier?" It does. You regain control, and the hacker's stolen keys are revoked.

## Why is this "Quantum Resistant"? 

You may hear that Pre-Rotation makes KERI "Post-Quantum Secure." Here is the simple reason why:

Quantum computers are predicted to break standard encryption, such as Elliptic Curve signatures easily. However, they struggle significantly with Hashes.

In KERI, your next key is protected by a Hash, not a Signature.
Even if a Quantum computer breaks your active key, it cannot reverse-engineer the Hash to find your next key.
This means your identity is safe even in a post-quantum world, giving you time to upgrade your security algorithms without losing your identifier.

## Recap 

Pre-Rotation transforms digital identity from a disposable asset (lose the key, lose the ID) into a persistent one. By separating the power to act (Signing) from the power to control (Rotation), KERI ensures that even if your device is hacked, your identity remains yours. This is the foundation of a truly durable digital reputation.

## Questions

1. In most digital identity systems, what happens if a hacker steals your private key?
A. **They can impersonate you, sign transactions, and lock you out**
B. Nothing, because keys can be changed instantly
C. The system automatically generates a new key for you
D. Your identity is temporarily suspended until you call a helpdesk

2. What is the core principle of Pre-Rotation?
A. Use the same key for signing and rotating for simplicity
B. **Don’t use the same key for signing and rotating**
C. Rotate keys every 24 hours automatically
D. Store all keys on the blockchain

3. In the “sealed envelope” analogy, what is published at inception?
A. Both Key Set A and Key Set B in full
B. Only the hash of Key Set A
C. **Key Set A in full and only the hash of Key Set B**
D. Neither key set – both remain hidden

4. Why is Pre-Rotation considered “quantum resistant”?
A. **The next key is protected by a hash, which quantum computers struggle to reverse**
B. It uses quantum computers to generate keys
C. It disables all encryption when a quantum attack is detected
D. It requires approval from a quantum-safe Certificate Authority

5. What are “hot” keys and “cold” keys in the context of Pre-Rotation?
A. Hot keys are used for encryption; cold keys are used for decryption
B. Hot keys are expired; cold keys are active
C. Hot keys belong to the issuer; cold keys belong to the holder
D. **Hot keys are active signing keys on your device; cold keys are hidden rotation keys kept offline**
