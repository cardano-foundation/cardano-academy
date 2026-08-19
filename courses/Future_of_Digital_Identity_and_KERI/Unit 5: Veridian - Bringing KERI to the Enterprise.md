# Veridian - Bringing KERI to the Enterprise

## The Enterprise Identity Dilemma

Enterprises today are stuck between a rock and a hard place.

* Option A: Centralized Identity (e.g., Active Directory). Problem: Vendor lock-in and single points of failure.
* Option B: Decentralized Identity (Web3). Problem: A chaotic mess of complexity and poor interoperability.

Veridian exists to solve this dilemma.

It is a platform designed to bring the power of decentralized identity to the enterprise, without the chaos. It wraps the raw power of the KERI protocol suite (KERI, ACDC, CESR) into a usable, scalable product for developers and businesses.

## The Strategic Pivot: Why Not Standard DIDs?

When building Veridian, we had to make a choice: Use standard Decentralized Identifiers (DIDs) or use KERI?

We evaluated the DID ecosystem and found a practical challenge for enterprise adoption:

* Interoperability: With over 200 DID methods across different chains, cross-chain identity verification requires complex bridging infrastructure.
* Operational Cost: Enterprises operating across multiple partners would need to support multiple chain backends — a significant infrastructure burden.
* Architectural Trade-offs: “Universal Resolvers” emerged to bridge methods, but they add a layer of intermediary infrastructure that KERI's design can bypass.

We chose KERI because it acts as a universal identity layer that can work alongside any blockchain, including Cardano, rather than competing with one.

You can think of KERI like TCP/IP for Trust. It doesn't care what network you are on. It creates a universal layer where any identity can verify any other identity, regardless of the underlying infrastructure.

## A New Foundation: Autonomic Trust

Most identity systems rely on Algorithmic Trust (trusting a blockchain).

Veridian relies on Autonomic Trust (trusting the Identifier).

* The Difference: In KERI, the identifier is self-certifying. Its validity is proven by its own cryptographic history (the Key Event Log), not by checking a ledger.
* The Benefit: This makes the identity Portable. You can move your corporate identity from a cloud server to a local data center without breaking it.

## Enterprise-Grade Features

Veridian selected KERI because its feature set maps directly to enterprise needs:

## 1. Solving Key Compromise (Pre-Rotation)

In traditional systems, if a corporate root key is stolen, it is a catastrophe. The company might have to revoke millions of credentials.

With Pre-Rotation, this becomes a manageable incident.

Because the "Rotation Key" is kept offline (cold storage), a hacker who steals the active "Signing Key" cannot take over the identity. The company simply uses the cold key to lock out the hacker and restore control.

## 2. Proactive Security (Watcher Network)

KERI uses a network of Watchers—think of them as a decentralized security team. They monitor the identifier's history 24/7. If an attacker tries to publish a fake history (duplicity), the Watchers detect it instantly, allowing the company to react before customers are harmed.

## 3. Governance (Multi-Signature)

Real businesses don't rely on one person with one key.

KERI supports Weighted Multi-Sig.
* For example, you can set a rule that says: "Signing a low-value invoice requires one key (The Manager). Signing a high-value contract requires a weight of three (The CEO + The COO + The CFO)."
This allows Veridian to mirror your actual corporate governance structure in code.

## 4. Verifiable Chains (ACDC)

Using ACDCs, we can build chains of trust.

* The Global Legal Entity Identifier Foundation, or GLEIF, Model: The Global Foundation delegates to an Issuer —> Issuer delegates to a Company —> Company delegates to an Employee. This creates a clear, audit-proof path of authority for every action taken by the enterprise.

## Recap

Veridian is the bridge between the bleeding edge of cryptography and the reality of enterprise business.

By choosing KERI, we avoid the "Blockchain Wars" and vendor lock-in. Instead, we provide a platform that offers:

* Security: Quantum-resistant Pre-Rotation.
* Governance: Native Multi-Signature support.
* Interoperability: A universal trust layer that works anywhere.

In the next units, we will dive deeper into the specific mechanics of these tools.

## Questions

1. What problem does Veridian solve for enterprises?<br>
A. It provides free cloud storage for all employees<br>
**B. It bridges decentralised identity and enterprise usability without the chaos**<br>
C. It replaces all existing enterprise software<br>
D. It eliminates the need for corporate governance<br>

2. Why did Veridian choose KERI over standard DIDs?<br>
**A. KERI acts as a universal identity layer that works alongside any blockchain**<br>
B. Standard DIDs are more expensive to implement<br>
C. KERI is the only protocol approved by the European Union<br>
D. Standard DIDs do not support any form of cryptography<br>

3. What does KERI’s Weighted Multi-Sig feature enable?<br>
A. Automatic deletion of old credentials<br>
B. Unlimited free transactions on any blockchain<br>
C. Anonymous voting in corporate elections<br>
**D. Different signing thresholds for different types of corporate actions**<br>

4. What is the role of the Watcher Network in Veridian?<br>
**A. It monitors identifier history and detects fake histories (duplicity) in real time**<br>
B. It provides customer support for identity issues<br>
C. It manages employee payroll<br>
D. It stores encrypted copies of corporate financial data<br>

5. KERI is compared to which foundational internet technology?<br>
A. HTML<br>
**B. TCP/IP**<br>
C. JavaScript<br>
D. HTTP cookies<br>
