# OOBI - Finding and Verifying Others

## The "Introduction" Problem 

In the traditional web, we trust URLs because a central authority, usually a DNS and/or Certificate Authority, vouches for them. If you see a lock icon on google.com, you trust it because a third party told you to.

But in KERI, there are no central authorities. We don't have a global phonebook. This creates a challenge: The Bootstrap Problem. If I hand you my digital identity, how do you find my keys? And more importantly, how do you know they are actually mine without asking a central server?

## The Solution: The OOBI 

KERI solves this with the OOBI (Out-of-Band Introduction). Don't let the acronym scare you. It simply means an introduction that starts "outside" the direct connection—like scanning a QR code, clicking a link in an email, or even typing in a URL manually.

Think of an OOBI as a Digital Business Card.

- **The Card (OOBI)** contains a pointer (URL) that says, "You can find my full records over here."
- **The Resume (KEL):** When you go to that address, you find the full Key Event Log (KEL)... this is the cryptographic proof of who I am.
- **The Difference** is that in the physical world, a business card can be faked. In KERI, the "card" leads to a history that is computationally infeasible to forge. 

## Types of Introductions 

There are two ways you usually encounter an OOBI:

- **Self-Introduction (SOOBI):** I show you my own QR code on my phone. "Here is my ID."
- **Third-Party Introduction:** Alice sends you a link to Bob's ID. "You should talk to Bob, here is his info."

## Security: Trust the Maths, Not the Messenger 

KERI is built on a Zero-Trust model. This is critical for OOBI. When your wallet scans a QR code, it assumes everything might be a trap:

- The QR code could be malicious.
- The server hosting the data could be hacked.
- The Wi-Fi you are using could be compromised.

It doesn't matter. Because KERI validates the History (KEL), not the Transport, the introduction channel is irrelevant. Your wallet downloads the KEL and checks the cryptographic signatures from the very beginning (Inception). If the maths adds up, the identity is valid, even if it was delivered by an enemy. This makes Man-in-the-Middle attacks useless, an attacker can't fake the maths.

## The OOBI in Action 

Here is what actually happens when you scan a QR code in the Veridian Wallet:

1. You scan a QR code, the OOBI.
2. Your wallet silently goes to the URL inside the code and fetches the identity's Key Event Log.
3. Your wallet runs the maths. It verifies every signature from the moment the ID was born until now.
4. Optionally, typically for high-security IDs, your wallet might ask the network's Witnesses (Notaries): "Is this the latest version of this ID?"
5. Only after all this maths passes does the wallet say "Connection Established."

## Recap 

The OOBI is the bridge between the physical world (a QR code) and the cryptographic world (the KEL). It solves the "Bootstrap Problem" by giving us a standardized, zero-trust way to start a conversation. Now that we know how to find people, the next step is exchanging data with them. 

## Questions

1. What does OOBI stand for?<br>
A. Online Operational Blockchain Interface<br>
B. Open Organisational Business Identifier<br>
C. **Out-of-Band Introduction**<br>
D. Offline Origin-Based Identity<br>

2. What is the “Bootstrap Problem” that OOBIs solve?<br>
A. **How to find someone’s keys and verify them without a central server**<br>
B. How to start a new blockchain from scratch<br>
C. How to install the Veridian wallet on a new phone<br>
D. How to convert physical documents to digital format<br>

3. Why doesn’t it matter if the OOBI delivery channel (e.g., a QR code) is compromised?<br>
A. Because OOBIs are encrypted with military-grade encryption<br>
B. Because QR codes cannot be tampered with<br>
C. Because the OOBI is stored on the blockchain for safety<br>
D. **Because KERI validates the history (KEL), not the transport channel**<br>

4. What is a SOOBI?<br>
A. **A Self-Introduction – showing your own QR code to someone**<br>
B. A government-issued OOBI with higher security<br>
C. A Secondary OOBI used for backup purposes<br>
D. A Standardised OOBI approved by GLEIF<br>

5. When you scan an OOBI QR code with the Veridian Wallet, what happens first?<br>
A. The wallet pays a gas fee to the blockchain<br>
B. The wallet calls a Certificate Authority to verify the code<br>
C. The wallet sends your private key to the other person<br>
D. **The wallet fetches the identity’s Key Event Log from the URL inside the code**<br>
