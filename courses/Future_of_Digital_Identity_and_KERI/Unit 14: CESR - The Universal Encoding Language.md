# CESR - The Universal Encoding Language

## Why Not Just Use JSON? 

In the web world, JSON is king. It's easy to read and works everywhere. But for high-security cryptography, JSON has a problem: it is "squishy." It requires a lot of processing power to parse, and it can be ambiguous, for example, in how it handles whitespace.

KERI needed something faster, stricter, and more secure. Enter CESR, which stands for Composable Event Streaming Representation. Think of CESR as the "Universal Grammar" of the KERI ecosystem. It is a language built from the ground up specifically for high-speed cryptography.

## "Smart Tags" (Qualified Primitives)
In standard systems, data is often just a blob of text. The software has to guess what it is. CESR changes this with Qualified Primitives. This core innovation makes every piece of data Self-Describing.

Think of it like a smart luggage tag on a suitcase.

The Tag or Derivation Code. It doesn't just say "Data." It says: "This is a Public Key (ie. its Type), using the Ed25519 algorithm (the Maths), and it is exactly 44 bytes long (the Size)."
The Bag (the Value): The actual cryptographic data follows immediately after.

For example, if you see the code ELvaU6...:

E tells the software: "I am a Blake3-256 Hash."
LvaU6... is the hash itself.

## Why "Crypto-Agility" Matters 

This tagging system solves a massive problem: Future-Proofing. In 10 years, when quantum computers break our current algorithms, most software will need to be rewritten. With CESR, we don't rewrite the system; we just introduce a new tag.

Today, we use Tag D for current encryption.
Tomorrow, we use Tag Q for Quantum-Safe encryption. The parser sees the new tag and automatically switches to the new maths library. The pipeline never breaks.

## Dual-Domain: Speaking Two Languages 

CESR is designed to be readable by both Humans and Machines. It supports two "Domains":

Text Domain for humans:
Uses text characters (Base64).
Why? You can open a file, read the logs, copy-paste keys, and debug issues easily.
Binary Domain for machines:
Uses raw bytes (0s and 1s).
Why? It is incredibly small and fast. This is what machines send "over the wire" to save bandwidth.

Crucially, you can convert between Text and Binary with zero loss. You can debug in Text, then compress to Binary for transmission.

## Composability 

The "C" in CESR stands for Composable. This means we can chain different pieces of data together into a stream without confusing the computer. Imagine a freight train. Because every car (data packet) has a "Smart Tag" saying exactly how long it is, the engine (CPU) acts efficiently:

Pipeline Processing: The CPU doesn't need to open the car to see what's inside. It reads the tag, sees "I am 100 bytes long," and instantly knows the next car starts at byte 101.
Early Rejection: If the engine sees a tag for a "Signature" but the data is corrupt, it can derail just that car—or the whole train—instantly, saving computing power. This protects the network from Denial-of-Service (DoS) attacks.

## Recap 

CESR is the "universal grammar" of KERI.

It's Precise: Every byte is accounted for using Smart Tags.
It's Agile: It can swap maths algorithms without breaking the system.
It's Fast: Machines can process it at lightning speed because it is self-describing.

By accepting a little more complexity in the encoding, we get a system that is secure enough for high-stakes identity and fast enough for the global internet.

## Questions

1. What does CESR stand for?<br>
A. Centralised Event Security Registry<br>
B. Cryptographic Encoding and Secure Relay<br>
C. Credential Exchange Standard for Rotation<br>
D. **Composable Event Streaming Representation**<br>

2. What is a “Qualified Primitive” in CESR?<br>
A. A raw data blob with no metadata attached<br>
B. **A self-describing piece of data with a tag indicating its type, algorithm, and size**<br>
C. A special encryption key used only for CESR data<br>
D. A standardised JSON field required in all KERI messages<br>

3. How does CESR achieve “Crypto-Agility”?<br>
A. **By using derivation code tags, so new algorithms can be introduced without rewriting the system**<br>
B. By locking the system to one encryption algorithm forever<br>
C. By converting all data to JSON before processing<br>
D. By requiring manual firmware updates to all devices<br>

4. What are the two “domains” that CESR supports?<br>
A. **Text domain (Base64, human-readable) and Binary domain (raw bytes, machine-optimised)**<br>
B. Public domain and private domain<br>
C. Internet domain and local domain<br>
D. Enterprise domain and consumer domain<br>

5. How does CESR’s composability help defend against Denial-of-Service (DoS) attacks?<br>
A. It blocks all incoming network traffic by default<br>
B. It requires attackers to solve a CAPTCHA before sending data<br>
C. It limits the total number of users on the network<br>
D. **Smart Tags let the CPU know packet sizes instantly, enabling early rejection of corrupt data**<br>
