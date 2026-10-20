# Chaining Credentials - Building Verifiable Trust

## Beyond a Single Credential 

So far, we have looked at credentials as single, standalone items. But in the real world, trust isn't solitary; it’s connected. A manager's authority comes from a director, whose authority comes from the board.

Traditional credentials act as "digital islands." A diploma might prove a student graduated, but it doesn't prove that the university itself is accredited. ACDC chaining solves this by building cryptographic bridges between these islands. It allows us to move beyond a single point of trust to construct a verifiable chain of trust.

## The Challenge: Limitations of the Basic Trust Triangle 

The standard model for digital identity is the "Trust Triangle" (Issuer → Holder → Verifier). This works for simple things, like a library card.

However, it has a critical flaw: it doesn't verify the Issuer. Imagine I set up a fake website called "Harvard Elite University" and issued you a credential. Technically, the credential is valid and my signature matches. But the university is a fraud. The Trust Triangle can't easily catch this. A verifier needs to know if the University itself is trusted.

## The Solution: ACDC Chaining 

To solve this, we use ACDC Chaining. This allows us to link credentials together into a "property graph." Think of it as the digital equivalent of a legal dossier. A notarized Power of Attorney (Credential A) is physically clipped to the Corporate Resolution that authorized it (Credential B), which is clipped to the Company's Incorporation Certificate (Credential C).

ACDC makes these "paperclips" cryptographic. By following the links, a verifier can trace authority from the user all the way back to a root of trust (like a government or global body).

## How "Edges" Work 

How do we actually link these files? We use a field in the ACDC structure called an "edge."
Think of an edge as a cryptographic hook. It connects one credential to another using a SAID (Self-Addressing Identifier).

The Hook (SAID): The edge contains the unique digital fingerprint of the target credential. Because it references the fingerprint, not a location, the link is unbreakable. If the target credential changes by even one byte, the fingerprint changes, and the chain breaks.
The Logic: Edges can enforce rules. For example, an edge can say, "This credential is only valid if the person holding it is also the Issuer of the credential above it." This allows for precise delegation of authority.
Real-World Application: The GLEIF vLEI Ecosystem 
The best example of this technology is the vLEI system, used to verify corporate identity.

The goal is to let a CEO sign a document and prove they have the authority to do so. The chain is built in four steps:

1. GLEIF (Root): The global root of trust issues a credential to a "Qualified Issuer."
2. QVI (Issuer): The Issuer now has a credential proving they are accredited by GLEIF.
3. Legal Entity (The Company): The Issuer gives a credential to the Company (e.g., Tesla). This credential links back to the Issuer.
4. OOR (The Role): The Company issues an "Official Organizational Role" credential to the CEO. This credential links back to the Company.

When the CEO signs a document, the verifier's software instantly crawls up this chain—from CEO to Company to Issuer to GLEIF—proving mathematically that the signature is valid. You may recognize this structure from earlier. That’s right, these digital chains form a DAG.

## Recap 

ACDC chaining turns a credential from a "digital sticky note" into a "digital chain of command." It proves not just what was said, but who gave the authority to say it. This capability is the key to building high-value trust systems, like secure supply chains or corporate identity.

## Questions

1. What limitation of the basic Trust Triangle does ACDC chaining solve? <br>
A. **It doesn’t verify the Issuer’s own legitimacy**<br>
B. It doesn’t encrypt the credential data<br>
C. It cannot handle more than two users<br>
D. It only works with physical documents<br>

2. What is an “edge” in the context of ACDC chaining?<br>
A. A web link to the issuer’s homepage<br>
B. **A cryptographic hook that connects one credential to another using a SAID**<br>
C. A physical USB cable connecting two devices<br>
D. A type of blockchain transaction<br>

3. Why is the SAID-based link described as “unbreakable”?<br>
A. It is protected by government regulation<br>
B. It is stored on multiple blockchains simultaneously<br>
C. **It references a unique fingerprint, so any change to the target invalidates the link**<br>
D. It is encrypted with a password only the issuer knows<br>

4. In the vLEI chain, what is the correct order from root to role?<br>
A. Legal Entity → QVI → GLEIF → OOR<br>
B. OOR → Legal Entity → GLEIF → QVI<br>
C. QVI → GLEIF → OOR → Legal Entity<br>
D. **GLEIF → QVI → Legal Entity → OOR**<br>

5. The linked structure of ACDC credentials forms which type of data structure?<br>
A. A circular linked list<br>
B. **A Directed Acyclic Graph (DAG)**<br>
C. A relational database table<br>
D. A binary search tree<br>
