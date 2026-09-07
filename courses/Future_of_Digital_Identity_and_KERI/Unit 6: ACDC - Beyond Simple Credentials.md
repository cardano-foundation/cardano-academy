# ACDC - Beyond Simple Credentials
The Next Generation of Verifiable Data 

While most are familiar with the concept of a simple, standalone digital credential (like a PDF course certificate), Authentic Chained Data Containers (ACDCs) offer a much more powerful framework. Defined by an emerging IETF specification, ACDCs move beyond isolated attestations to enable complex, verifiable data relationships.

An ACDC is a container designed to prove exactly who authored data and where it came from. These containers are structured as Directed Acyclic Graphs (DAGs). While the term sounds complex, the concept is straightforward: it is a method of linking data where "arrows" only point one way. This prevents circular logic and ensures a clear flow of information.

Each ACDC acts as a "node" that connects to other containers via cryptographically verifiable links, or "edges." This allows us to build digital structures that mirror real-world hierarchies.
The ACDC Advantage: Key Differentiators from W3C Verifiable Credentials 

The design of the ACDC protocol unlocks security and flexibility capabilities that other formats struggle to match. The key advantages over standard W3C Verifiable Credentials include:

Schema Referencing (No Link Rot): Standard credentials often use web links (URLs) to define their structure. If that website goes offline or the file moves, the credential breaks. ACDCs avoid this by using a Content-Addressable Secure Hash, aka Self-Addressing Identifiers (SAID), which we expand on later. The rules are locked mathematically, not hosted on a server, ensuring the credential remains valid for decades.
Scope of Use: ACDC is flexible. It supports both targeted credentials (issued to a specific person) and untargeted, signed documents (like a public audit report).
Data Chaining: This is the killer feature. ACDCs are designed to be linked together to form chains. This enables us to model provenance (history) and delegation (permission).


Unlocking Advanced Use Cases with ACDC Chaining 

The true power of an ACDC lies in its "edge" section—cryptographic pointers that allow one credential to reference another. By linking credentials, we create a provable line of authority.

Consider a government authority issuing an Accreditation Credential to a University. The University then issues a Diploma Credential to a Student.

The diploma uses an "edge" to point back to the University's accreditation.
When an employer verifies the diploma, the software automatically crawls up the chain.
It confirms not only that the diploma is valid, but that the University was accredited at the time of issuance.

This chaining capability unlocks:

Cryptographic Provenance: A tamper-evident chain of custody, vital for supply chains.
Delegated Authority: Proving that a manager has the specific authority (delegated from a director) to sign a purchase order.
Complex Logic: Chains can include rules. For example, "This Purchase Order is valid ONLY if signed by a manager with a "Budget Authority" credential."
ACDC in Action: The GLEIF vLEI 

The best real-world example of this architecture is the verifiable Legal Entity Identifier (vLEI) system.

The vLEI uses a chain of ACDC credentials to represent corporate authority:

GLEIF (Root): The global root of trust.
QVI (Issuer): A "Qualified vLEI Issuer" accredited by GLEIF.
Legal Entity: The company itself.
OOR (Role): An "Official Organizational Role" credential held by an individual, for example, a CEO.

This structure allows a CEO to digitally sign a document and prove—mathematically—that they have the authority to act on the company's behalf. This model is now an ISO standard (ISO 17442-3).
Recap 

Authentic Chained Data Containers are more than just a replacement for digital badges. They are a data structure that understands context. By using ACDCs, Veridian ensures that every piece of data has a verifiable history. It transforms identity from a static claim into a verifiable chain of trust that can support legally binding digital interactions.

Questions

1. What does ACDC stand for?
Authentic Chained Data Containers
Automated Credential Distribution Chain
Advanced Cryptographic Data Certificates
Autonomic Credential Delivery Channels

2. How are ACDCs structured?
As Directed Acyclic Graphs (DAGs) with one-way links
As flat, standalone PDF files
As circular reference chains
As simple key-value pairs stored in a database

3. How do ACDCs avoid “link rot” compared to standard W3C Verifiable Credentials?
They store all data on a central web server with guaranteed uptime
They use Self-Addressing Identifiers (SAIDs) instead of web URLs for schema referencing
They require annual renewal from the issuer
They use blockchain-hosted URLs that never change

4. What is the “killer feature” of ACDCs?
They can be printed on paper
They are free to issue and verify
Data chaining – the ability to link credentials together to model provenance and delegation
They work without any cryptography

5. In the vLEI example, what does the OOR credential represent?
A company’s financial audit report
A software license for the Veridian platform
A blockchain transaction receipt
An Official Organisational Role held by an individual, such as a CEO
