# SAIDs - The Root of Data Integrity

## The "Label on the Jar" Problem 

In most systems, an Identifier (ID) and the Data it points to are separate.

- The ID: Record_123
- The Data: Name: Alice 

The problem is that Record_123 is just a random label. If a hacker changes the data to Name: Bob, the ID is still Record_123. There is no mathematical link between the label and the contents of the jar.

## The "Recursive" Paradox 

To fix this, we usually use Cryptographic Hashes. Think of them as digital fingerprints. If you change one letter of the data, the fingerprint changes completely. But this creates a paradox: Where do you store the fingerprint? You can't write the fingerprint inside the file, because writing it changes the file, which changes the fingerprint. It’s an infinite loop. It’s like trying to take a Polaroid picture that includes the photo you are currently taking.

## The SAID (Self-Addressing Identifier) 

KERI solves this with the SAID. It allows us to put the ID inside the data it identifies. This seems impossible, but KERI uses a clever "Placeholder" trick to do it.

Here is how KERI calculates a SAID in five steps:

Prepare: Take the data (for example, a JSON file).
Placeholder: In the spot where the ID will go, insert a "dummy" string of dummy characters (e.g., ################).
Hash: Calculate the hash of the file including the dummy characters.
Embed: Take that resulting hash and overwrite the dummy characters with it.
Result: You now have a file that contains its own ID.

## Verification: The Reverse Trick 

How do you verify this?

- You receive the file.
- You copy the ID and set it aside.
- You fill the empty spot with the "dummy" characters again.
- You run the hash maths.
- Check does your new hash match the ID you set aside? If yes, the data is perfect. If even one bit has changed, the maths will fail.

## Why This Matters 

This "Magic Trick" is the foundation of KERI's security.

It’s Tamper-Proof. The ID is cryptographically bound to the content. You cannot alter the data without invalidating the ID.
It’s Self-Contained. You don't need an external database to check if the data is valid. The file itself contains the proof of its own integrity.
SAIDs in Action 

You will see SAIDs everywhere in the Veridian ecosystem:

1. **Key Event Logs:** Every event in your history is linked to the previous one using SAIDs. This creates an unbreakable chain.
2. **Schema Security:** How do we know a credential follows the rules? The schema is identified by a SAID. If someone tries to change the rules (a "bait and switch"), the SAID changes, and the fraud is detected.
3. **Privacy:** Because every part of a document has its own SAID, you can selectively reveal parts of a document while keeping others private, and the maths still holds up.

## Recap 

The SAID is the "atom" of the KERI universe. By solving the paradox of embedding a hash inside the data it hashes, it allows data to be Self-Verifying. 

## Questions

1. What problem does a SAID solve?<br>
A. **The lack of a mathematical link between an identifier and the data it labels**<br>
B. The need for faster internet connections<br>
C. The difficulty of printing QR codes on paper<br>
D. The cost of storing data in the cloud<br>

3. What does SAID stand for?<br>
A. Secure Automated Identity Document<br>
B. **Self-Addressing Identifier**<br>
C. System-Assigned Identity Descriptor<br>
D. Standard Authentication and Integrity Digest<br>

4. How does KERI solve the “recursive paradox” of embedding a hash inside the data?<br>
A. It stores the hash externally on a separate blockchain<br>
B. It avoids using hashes altogether<br>
C. It requires a central server to compute and store the hash<br>
D. **It uses a placeholder trick – inserting dummy characters, hashing, then replacing the placeholder**<br>

5. How does a verifier check that a file with a SAID has not been tampered with?<br>
A. They call the issuer and ask for confirmation<br>
B. They compare the file to a copy stored on a central server<br>
C. **They replace the SAID with dummy characters, re-hash, and check if the result matches**<br>
D. They scan the file with antivirus software<br>

6. How do SAIDs enable selective disclosure and privacy?<br>
A. They encrypt all data so no one can read it<br>
B. **Every part of a document has its own SAID, so parts can be revealed while others stay private**<br>
C. They delete sensitive data after verification<br>
D. They require a VPN to access any credential<br>
