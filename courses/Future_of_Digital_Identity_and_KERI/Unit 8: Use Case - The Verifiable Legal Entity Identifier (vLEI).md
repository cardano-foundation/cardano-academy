# Use Case - The Verifiable Legal Entity Identifier (vLEI)

## The Problem: Who are you, really? 

In the physical world, verifying a business is relatively easy—you can check a corporate seal, visit an office, or meet a director. But online, we rely on weak evidence: domain names, email signatures, and PDF letterheads. All of these are easily forged.

This lack of a secure standard is the root cause of "Business Email Compromise" (BEC) and invoice fraud. If you receive an email from "The CEO," how do you prove it’s actually them?

## The Solution: The vLEI 

The internet needs a standard for organizational identity. The Verifiable Legal Entity Identifier (vLEI) is exactly that.

Think of the vLEI as a digital passport for a company. It allows an organization to prove its identity—and the authority of its employees—instantly and mathematically. It replaces the "trust me" of an email signature with the "verify me" of cryptography.

## The Legitimacy:

ISO Standard: It isn't a proprietary tech experiment; it's an ISO standard (ISO 17442-3). (show faint ‘International Organization for Standardization’ on screen)
GLEIF Governance: It is managed by the Global Legal Entity Identifier Foundation (GLEIF), the same G20-backed body that manages financial identifiers for the world's markets.
Powered by KERI: It uses KERI for security and ACDC for the credentials.

## The Architecture: The Chain of Authority 

The vLEI isn't just a single ID; it is a hierarchy. It mirrors the real-world chain of command.

The ecosystem is built in tiers:

GLEIF (Root): The global anchor of trust.
Qualified vLEI Issuers (QVIs): Organizations vetted by GLEIF to issue credentials (like a digital notary).
Legal Entities: Companies (e.g., a bank or a supplier) receive a vLEI credential.
Organizational Roles (OOR): The company issues credentials to people, like a "CEO" or "Accounts Payable Manager."

## How it Works in Practice 

Imagine a CEO needs to sign an annual report.

The CEO uses their OOR Credential to sign the PDF.
Anyone who opens that PDF can verify the signature.
The verification software traces the chain: CEO → Company → Issuer → GLEIF.
If any link in that chain is broken (e.g., the company's status was revoked), the signature shows as invalid.

## Why KERI? (Strategic Implications) 

You might ask: Why did a global body like GLEIF choose KERI?

Key Rotation: Corporate keys are high-value targets. KERI’s "pre-rotation" feature protects them better than standard blockchain wallets.
Historical Validity: In many systems, if you change your key, your old signatures become invalid. KERI uses a Key Event Log to prove that a signature was valid at the time it was signed, even if the keys have changed since. This is critical for legal documents that must last for decades.
Interoperability: With many competing DID methods, KERI provides a unifying identity layer that works across different ecosystems.

## Recap 

The vLEI is the first global, standardized implementation of decentralized identity. It moves us from administrative trust ("I trust this database") to cryptographic trust ("I verified the mathematical proofs").

For organizations using Veridian, this means you can finally retire the insecure PDF scan. Instead, you can issue digital credentials that prove—undeniably—who you are and what you are authorized to do.

## Questions

1. What real-world problem does the vLEI primarily address?<br>
A. Slow internet speeds for enterprise users<br>
B. **The inability to securely verify business identity and employee authority online**<br>
C. The high cost of office supplies for large corporations<br>
D. Difficulty in hiring qualified IT staff<br>

2. Which ISO standard applies to the vLEI?<br>
A. ISO 9001<br>
B. ISO 27001<br>
C. **ISO 17442-3**<br>
D. ISO 14001<br>

3. What is a Qualified vLEI Issuer (QVI)?<br>
A. A government agency that prints physical ID cards<br>
B. A blockchain mining pool<br>
C. A software company that builds wallet applications<br>
D. **An organisation vetted by GLEIF to issue vLEI credentials**<br>

4. Why is KERI’s Key Event Log important for legal documents?<br>
A. **It proves a signature was valid at the time it was signed, even after keys change**<br>
B. It translates documents into multiple languages<br>
C. It automatically files documents with the court<br>
D. It reduces the file size of PDF documents<br>

5. Which G20-backed body manages the vLEI system?<br>
A. The World Bank<br>
B. The International Monetary Fund<br>
C. **The Global Legal Entity Identifier Foundation (GLEIF)** <br>
D. The United Nations Development Programme<br>
