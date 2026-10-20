# The ToIP Stack - Placing KERI in Context

## The Internet's Missing Floor 

The Internet has a "Missing Layer." We have a standard way to move data packets with TCP/IP, but we have no standard way to know who sent them. Because of this, we rely on Google, Facebook, and Banks to be the "Trust Police."

The Trust over IP (ToIP) Foundation, part of the Linux Foundation, was created to fix this. They built a blueprint for how to add a "Trust Layer" to the internet.

## The Blueprint: Wet Code vs. Dry Code 

ToIP recognizes that trust isn't just technology. It splits the problem into two parallel stacks:

Dry Code (Technology): The servers, cryptography, and protocols. This is what machines read.
Wet Code (Governance): The policies, contracts, and human rules. This is what lawyers and business people read. Key Insight: You cannot build a trust network with just software. You need the "Wet Code" to define the rules of the game.

## The 4 Layers of the Stack 

The Technology side is divided into four layers, like a building:

Layer 1 - Utilities are like the foundation. This is where Identifiers (DIDs) live. Usually, this is a blockchain.
Layer 2 - Communication, like the plumbing. This is how two people talk securely, peer-to-peer, using wallets.
Layer 3 - Exchange: Think of it as being like commerce. This is where we trade Credentials, like a Driver's License or a Diploma.
Layer 4 - Ecosystems is the penthouse in our analogy. These are the actual apps that use the layers below. Use cases such as Healthcare, Finance, Supply Chain, etc.

## Where Does KERI Fit? 

KERI is unique because it changes how we build Layer 1.

## Layer 1: The Autonomic Foundation 

In most systems, Layer 1 relies on a blockchain — Ethereum, Cardano, Hyperledger — for anchoring identifiers. KERI can use these chains for timestamping and anchoring events, but it doesn't depend on any single one for security. This means KERI identities can leverage Cardano's strengths while remaining portable. In KERI, Layer 1 is You. Because KERI identifiers (AIDs) are self-certifying (backed by your own Key Event Log), we don't strictly need a blockchain. We can use one to timestamp events, but we don't depend on it for security. This makes KERI portable and cheap.

## Layer 2: The Trust Spanning Layer 

This is the "Narrow Waist" of the hourglass model. KERI uses OOBIs (QR codes) to connect wallets directly. It creates a secure, private tunnel between two people without a middleman.

## Layer 3: ACDC & IPEX 

This is where the "Trust Triangle" happens.

The Object: We use Authentic Chained Data Containers (ACDCs) as the credentials.
The Delivery Truck: We use IPEX, or the Issuance and Presentation Exchange, as the protocol to deliver those credentials securely. Think of it as a communication framework for negotiating the secure exchange of verifiable credentials, VCs, between different parties.

## Layer 4 in Action: The vLEI 

The best real-world example of this entire stack is the GLEIF vLEI.

Layer 1: KERI AIDs for companies.
Layer 2: Secure connections between company wallets.
Layer 3: Exchanging vLEI Credentials (ACDC).
Layer 4: Using those credentials to sign Annual Reports (The App).
Wet Code: The GLEIF Governance Framework (The Rulebook).

## Recap 

Think of the Trust Over IP (ToIP) stack as the map, and KERI as the engine. By fitting KERI into this standardized model, we ensure that the identity systems we build aren't just isolated islands, they are compatible with the future of the global internet.


## Questions

1. What does the Trust over IP (ToIP) Foundation aim to fix?<br>
A. The slow speed of internet connections worldwide<br>
**B. The internet’s lack of a standard trust layer for verifying identity** <br>
C. The incompatibility between Mac and Windows operating systems<br>
D. The high cost of domain name registration<br>

2. In the ToIP model, what is “Wet Code”?<br>
**A. Policies, contracts, and human governance rules**<br>
B. Software code that runs on underwater servers<br>
C. Code that processes liquid asset transactions<br>
D. Temporary code that is deleted after execution<br>

3. At which layer of the ToIP stack does KERI change the traditional approach?<br>
A. Layer 4 – Ecosystems<br>
B. Layer 3 – Exchange<br>
C. Layer 2 – Communication only<br>
**D. Layer 1 – Utilities (the identifier foundation)** <br>

4. What protocol does KERI use at Layer 3 for credential exchange?<br>
A. HTTP and HTTPS<br>
**B. IPEX (Issuance and Presentation Exchange)** <br>
SMTP (Simple Mail Transfer Protocol)<br>
FTP (File Transfer Protocol)<br>

5. In the ToIP framework, which layer represents the actual end-user applications?<br>
A. Layer 1 – Utilities<br>
B. Layer 2 – Communication<br>
C. Layer 3 – Exchange<br>
**D. Layer 4 – Ecosystems** <br>
