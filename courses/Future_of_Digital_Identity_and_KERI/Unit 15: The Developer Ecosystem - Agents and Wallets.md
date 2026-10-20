# The Developer Ecosystem - Agents and Wallets

## From Theory to Code 

We have covered the theory of KERI. Now, how do we actually build applications with it? This unit is about your Developer Toolbox. Instead of writing complex cryptography from scratch, the Veridian ecosystem gives you ready-made components: Wallets for your users and Cloud Agents for your backend.

## The Core Architecture: “Remote Control” Model

The most important design choice in Veridian is Edge Control. We separate the system into two parts:

1. The Edge (The User):
- What it is: The mobile app or browser client, using the Signify library.
- What it does: It holds the Private Keys. All signing happens here.
- Analogy: This is the "Remote Control." It has the buttons and the authority.

2. The Cloud (The Infrastructure):
- What it is: The server running the KERIA agent.
- What it does: It stores the logs (KELs) and routes messages to other people.
- Analogy: This is the "TV." It displays the content and connects to the cable network, but it cannot change channels itself.

Why is it set up like this? Well, for security mostly. Because the Private Keys never leave the "Edge" (the user's device), hackers can compromise the entire cloud server and steal... nothing. They get encrypted logs, but they cannot impersonate a single user.

## The Veridian Wallet: The User's Gateway 

For the end-user, this complexity is hidden behind the Veridian Wallet.

ID Management: It manages the keys for their Identity (AID).
Recovery: During setup, the user gets a 18-word recovery phrase (BIP 39). This is the "Master Key." If they lose their phone, this phrase regenerates their keys.
Connections: It scans QR codes (OOBIs) to connect with others.

## The Developer's Toolkit: KERIA & Signify 

As a developer, you won't be writing raw KERI code. You will use two tools:

## 1. KERIA (The Muscle)

This is the backend server. It is "Multi-Tenant," meaning one server can support thousands of users.

It acts as a mailbox for messages.
It acts as a backup hard drive for Key Event Logs.

## 2. Signify (The Brain)
This is the client-side library (available in TypeScript and Python).

It runs inside your app (mobile or web).
It handles the maths. It generates keys and signs messages before sending them to KERIA.

## Code Example: The Handshake 

Here is how you connect a user (Signify) to the cloud (KERIA) in TypeScript:

import { SignifyClient, ready, Tier } from "signify-ts";

// 1. Load the crypto library (libsodium)
await ready();

// 2. Configure the client
const client = new SignifyClient(
  config.keria.url,
  randomPasscode(), // The user's secure passcode
  Tier.low,
  config.keria.bootUrl
);

// 3. The Handshake
await client.boot();

What does boot() do? This is the critical step. boot() tells the KERIA server: "I am a new user. Please create a private agent instance just for me." In response, KERIA spins up a dedicated database and agent ID for that specific user. This ensures that User A's data is completely isolated from User B's data, even if they use the same server.

## Polyglot Development 

While Python (KERIpy) is the reference implementation, the ecosystem speaks many languages:

- TypeScript/JS: KERIjs / Signify-TS (For Web & Node)
- Rust: KERIox (For high performance)
- Java: Signify (for backend)
- Go: KERIgo (For backend services)
- Swift: KERIml (For iOS apps)

## Recap 

The Veridian ecosystem is designed to make KERI easy for builders.

Signify handles the Keys (Edge).
KERIA handles the Traffic (Cloud). 

By using these tools, you can build apps that are secure by default, without needing a PhD in cryptography.


## Questions

1. In Veridian’s “Remote Control” model, where are the private keys stored?<br>
A. On the KERIA cloud server<br>
B. In a centralised key management service<br>
C. On the blockchain<br>
D. On the edge – the user’s device (mobile app or browser)<br>

2. What is KERIA?<br>
A. A mobile wallet application for end users<br>
B. A programming language for writing smart contracts<br>
C. A multi-tenant backend server that stores logs and routes messages<br>
D. A type of cryptographic hash algorithm<br>

3. What does the boot() command do when a Signify client connects to KERIA?<br>
A. It downloads the entire blockchain to the user’s device<br>
B. It tells KERIA to create a dedicated agent instance and database for the new user<br>
C. It generates a new blockchain address for the user<br>
D. It deletes the user’s previous identity records<br>

4. Why does Veridian’s architecture keep private keys on the edge device?<br>
A. So that even if the entire cloud server is compromised, no user can be impersonated<br>
B. To save cloud storage costs<br>
C. Because edge devices have faster processors<br>
D. Because cloud servers cannot perform cryptographic operations<br>

5. What recovery mechanism does the Veridian Wallet use?<br>
A. Email-based password reset<br>
B. An 18-word BIP 39 recovery phrase<br>
C. Fingerprint scanning at a verified kiosk<br>
D. Calling customer support to verify your identity<br>
