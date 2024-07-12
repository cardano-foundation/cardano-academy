# Unit 4 - Public Key Encryption

## Learning Objectives
By the end of this unit, the learner should be able to:
Describe and compare encryption types
Explain the process of encryption using an example
Describe attack models
Compare the two leading encryption algorithms

Introduction
Hello everyone, and welcome. My name is [lecturer name], and I’ll be your lecturer today.
Table of Contents
In this unit, we explore encryption methods, a major part of cryptography. 

This lecture will introduce some technical concepts and terminology. Feel free to pause at any point and review. 

Let’s start with terms.

Cryptography is the science; encryption is the method.

Encryption is the process of encoding understandable text into something you can’t understand. Technically, encryption is encoding cleartext, what you understand, into ciphertext. The reverse process, transforming ciphertext into cleartext, is decryption. 
An Encrypted Communication System
The diagram below shows an encrypted communication system. Alice wants to send Bob a message, but she doesn’t want anyone, like untrusted third parties or adversaries, to read it. Alice encrypts the cleartext and sends the generated ciphertext over the communication channel to Bob. Bob receives the ciphertext, decrypts it into cleartext, and then reads it.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/1.4.1.png)

## An Encryption Scheme
Alice and Bob took several steps to ensure their conversation was private. The first step involved encrypting their data. To do this, they needed an encryption algorithm, which converted their original message into secret and uninterpretable ciphertext. This ciphertext looked like a series of random numbers and letters, like ‘ABC123DEF789’.

To use the encryption algorithm, they also needed a key. This key was kept secret and allowed only the participants in the conversation to decrypt the message. Having a key means that the encryption and decryption algorithms can be open for anyone to inspect. 
The key appeared as a series of random ones and zeros, each one corresponding to a bit. The total number of bits in a key is known as the key size. For example, a key with a key size of 20 bits might look like ‘0001 0101 1110 1100 0110’.

Let’s sum up the encryption using logic:
Message m plus an encryption key k processed by the encryption algorithm e creates ciphertext c.


A Decryption Scheme
Alice’s message is encrypted. Even if an adversary can access the ciphertext, they won’t be able to interpret or decipher the message. So far so good. But how does Bob, the intended recipient, read the message? For that, using our logic statement, Bob the receiver needs a decryption algorithm and a key.


Symmetric Encryption
There are two types of algorithms for encrypting messages: symmetric encryption and asymmetric encryption. In symmetric, the same key is used to encrypt and decrypt the data, making it fast and simple but less secure. Asymmetric, also known as public key cryptography, uses two keys: a public key and private key. What one key can encrypt, the other can decrypt.

Symmetric encryption algorithms take as parameters the cleartext message, and a key. The resulting ciphertext is sent to the receiver, where the original cleartext message can be decrypted using the same key the sender used to encrypt the message. 


Symmetric-Key Algorithms
There is a wide range of symmetric-key algorithms, such as DES, 3DES, AES, IDEA, CAST5. Twofish, Serpent, Camellia, Blowfish, Kuznyechik, and Safer [ref.4.1.1]. 

Data Encryption Standard (DES) was the first to be adopted. It was developed in the 1970’s by IBM with the National Security Agency. DES became a federal standard for shared-key encryption from 1973 until 1997, when it was considered cryptographically compromised and deprecated, meaning its use was no longer recommended. The Advanced Encryption Standard – or AES – replaces DES
Asymmetric Encryptions
In all symmetric-key algorithms the sender and the receiver both require knowledge of the selected algorithm and key prior to communication. Symmetric-key algorithms therefore assume that both parties securely exchange the key outside the message channel, prior to setting up the encrypted communication. They could meet in person, for example, and exchange the key. This is called a “key exchange” challenge.

Asymmetric encryption, or public key cryptography, does not require a shared key. Instead, both parties generate their own private key and never share it with anyone. Yet, each also generates an associated public key from their private key. That public key is meant to be shared. The two keys together form a public/private key pair.



If Alice wishes to communicate with Bob, she will encrypt her cleartext message using Bob's public key. Alice can now send the encrypted ciphertext message to Bob.

Bob and Alice each have a private key and public key, just like any other user on a network. The public keys are available for anyone to use to encrypt a message. The private keys are never shared. Any cleartext encrypted with a public key can be decrypted using its corresponding private key. Similarly, any cleartext encrypted with the private key can be decrypted with the corresponding public key. We call that latter operation a digital signature and we’ll expand on this concept in the next unit.

Let’s walk through the example. If Bob wants to receive a message from Alice, he will share his public key. Bob's private key will never leave his system.

Meanwhile, Alice will use Bob’s public key to encrypt the cleartext and send the encrypted message or ciphertext to Bob. Bob will then decrypt the ciphertext using his own private key. If an adversary intercepts a copy of the encrypted message, it’s not a problem. The adversary cannot decrypt the ciphertext because they do not have Bob's private key. Also, if we assume the adversary has knowledge of Bob's public key, it is still impossible to generate Bob's private key. A private key can be used to generate the public key but not vice-versa, it is a one-way operation similar to a hash function.
Asymmetric-Key Algorithms
There are many asymmetric encryption algorithms, some more commonly used than others. Like the Rivest Shamir Adleman (RSA) and the Elliptical Curve Cryptography (ECC).

Rivest Shamir Adleman, or RSA, is one of the oldest asymmetric encryption algorithms. It was published in 1977 by Ron Rivest, Adi Shamir, and Leonard Adleman [ref.4.1.2]. RSA generates a private key by multiplying two random prime numbers together in a logarithmic formula, making it complex but fast. The public key is derived from a component of this formula. This means the private key can decrypt a message created with the public key but not the other way around.

A faster and smaller alternative to RSA is the Elliptical Curve Cryptography, or ECC. It uses mathematical elliptic curves with smaller key sizes and is considerably faster than RSA when it comes to key and digital signature generation. It has become a popular choice for signing cryptocurrency transactions for this reason. Bitcoin uses the Elliptic Curve Digital Signature Algorithm, or ECDSA, to digitally sign transactions and ensure that funds are only spent by authorized users.

Note that adversaries will still attempt to break an encryption algorithm without knowledge of the key pair. They likely have some degree of access to one source of information or another. For this reason, encryption is only as good as the algorithm and the ability of the user to keep the private key safe.
CPA-Secure Encryption Algorithm
Let’s look at some different attack models hackers might use to break encryption.

The simplest attack model is Chosen Plaintext Attack (CPA). In this attack, the attacker can run encryption algorithms on a computer but can't see the secret key. The attacker picks two messages, m and m', and sends them to the computer. The computer then chooses a random number and encrypts the messages to make c1 and c2. The attacker's job is to guess which encrypted message is m and which is m'.

The property of being unable to distinguish pairs of ciphertexts based on the message they encrypt is called semantic security, or indistinguishability.


CCA-Secure Encryption Algorithm
The Chosen Ciphertext Attack (CCA), is another type of attack. In this approach, the attacker has access to both an encryption and a decryption computer. The attacker picks a few messages, and the computer turns them into a secret code, ciphertext c. The attacker can ask the computer to decode the ciphertext and try to guess the secret key.

This attack model is known as Indistinguishability under a Chosen Ciphertext Attack (IND-CCA). There are two versions of this attack: adaptive and non-adaptive. In non-adaptive, also known as the Lunchtime Attack or IND-CCA1, adversaries can only make decryption requests before seeing the ciphertext c that they are trying to break. In the adaptive variant IND-CCA2, they can continue to make decryption requests even after seeing the ciphertext c provided they do not request to decrypt c itself – otherwise the attack would be trivial. [ref 4.1.3]. In practice, this attack model illustrates the case where an attacker might have gotten access to a list of encrypted messages alongside their non-encrypted sources. Encryption algorithms that are resistant to IND-CCA1 and IND-CCA2 ensures that it is infeasible from an attacker with this added knowledge to break the encryption of another ciphertext. 


Cryptographic Assumptions and Quantum Computing
Encryption schemes are based on mathematical assumptions. For example, the RSA assumes that it is computationally difficult to calculate the prime factors used in the secret key generation process. A computer would need  to try every prime number to determine the possible factors – an exceedingly time-consuming task. However, quantum computers can factorize numbers far more efficiently using algorithms such as Shor’s algorithm. This means that many encryption algorithms, including RSA and ECC, will be easily broken when quantum computers become available in the market. 

There are several quantum-safe asymmetric algorithms already being developed, such as the hash-based encryption method. This hash-based encryption method, however, uses a larger key size than ECC and so it is not widely used at present. The symmetric encryption family does have several quantum-safe algorithms too, such as AES-256 and Twofish-256, but more alternatives are still required. That’s what makes quantum cryptography important for the future of blockchain. For our purposes, with today’s common computers, private keys are highly unlikely to be generated using a public key. Most of the time, humans are still the weakest link. Private keys must be kept as secure as possible.

Relying on asymmetric encryption might seem like the best option. However, asymmetric encryption needs far more computational power than symmetric encryption. In addition, with the same key size, asymmetric encryption is usually easier to break than a symmetric key. On the other hand, asymmetric encryption does not have the key exchange challenge associated with the shared symmetric encryption keys. 

To address all this, the process in a communication system is usually done in two phases. First, a symmetric encryption key will be exchanged using asymmetric cryptography. This key is commonly referred to as the session key. In the second phase, both sender and receivers switch to a symmetric algorithm to encrypt the entire communication.  

The diagram below shows the process. It goes like this:
Bob sends his asymmetric public key to Alice.
Alice chooses a symmetric key and encrypts it using Bob’s asymmetric public key.
Bob then receives the encrypted message and decrypts it with his own asymmetric private key. The decrypted message contains Alice's symmetric key, which is called the session key.
Bob now switches to symmetric encryption and uses the shared symmetric key from Alice – or session key – to encrypt the message.
Bob sends the symmetrically encrypted message ciphertext to Alice.
Finally, Alice decrypts the received message ciphertext using the shared symmetric key and algorithm.

As you see, in this mechanism Alice and Bob used an interactive method to exchange a secret key, and then used a symmetric encryption algorithm using the exchanged secret key for the rest of communication. This is actually how most of the encryption works on the Internet. When you access a website through ‘https’, your browser negotiates a session key with the server using asymmetric cryptography and then relies on symmetric encryption throughout.


Review
And that’s it, we’ve reached the end of this lecture. Let’s review what we have covered:

In this unit, we explored how data can be encrypted using different encryption algorithms. We looked at how encryption algorithms work in theory and from a practical perspective. Finally, we considered how symmetric and asymmetric encryption compliment each other.

Next, we will look into how to secure the actual transmission of public keys.

One final note: We introduced several new concepts and terminology throughout this lecture. We encourage you to go back, review them, and then explore them further. 

See you next time.
References
[Ref.4.1.1] Cornell University, “Symmetric-Key Cryptography”, Available:  http://www.cs.cornell.edu/courses/cs5430/2010sp/TL03.symmetric.html , Accessed: 17 Dec 2022.
[Ref.4.1.2] Rivest, R. L., Shamir, A., and Adleman, L. "A method for obtaining digital signatures and public-key cryptosystems." Communications of the ACM 21, no. 2, pp. 120-126, 1978.
[Ref 4.1.3] Katz, Jonathan and Lindell, Yehuda. Introduction to Modern Cryptography. 2nd Edition, Chapman & Hall, 2015.

Questions
Sub-Unit 1
Which of the following images accurately depicts the flow of an encryption scheme? (Image Question)






What is the role of the encryption key in the encryption process?
It serves as a delivery address to send the message to
It determines how much of the ciphertext will be revealed
It allows only the participants in the conversation to decrypt the message (CORRECT ANSWER)

Sub-Unit 2
Symmetric encryption uses two different keys to encrypt and decrypt the data respectively.
TRUE
FALSE (CORRECT ANSWER)


Select the correct statement about symmetric encryption algorithms.
They require no coordination between participants
They are a fast and easy way to encrypt a cleartext message (CORRECT ANSWER)
They are less likely to be decrypted by adversaries than other encryption algorithms


What type of encryption algorithm does the following image depict? (Image Question)

A symmetric-key algorithm (CORRECT ANSWER)
An asymmetric-key algorithm
This could be either a symmetric or an asymmetric key algorithm
Sub-Unit 3
Encryption encodes a message into text that can’t be understood. In asymmetric encryption:
Both the sender and the receiver share a private key
There is only one key to encrypt and decrypt the message
Both private keys and public keys can be used to encrypt and decrypt messages (CORRECT ANSWER)
Messages can only be encrypted with a private key


A private key should be shared with the recipient of the message.
TRUE
FALSE (CORRECT ANSWER)


In public key cryptography, both parties generate their own private key and associated public key from their private key. 
TRUE (CORRECT ANSWER)
FALSE


How does asymmetric encryption differ from symmetric encryption regarding key sharing?
Asymmetric encryption requires the exchange of a shared key
Asymmetric encryption uses a private key for encryption and a public key for decryption
Asymmetric encryption does not require sharing a private key, but the public key is meant to be shared (CORRECT ANSWER)

Sub-Unit 5
The Elliptic Curve Digital Signature Algorithm (ECDSA) is an example of symmetric key algorithms.
True
False (CORRECT ANSWER)


Which asymmetric encryption algorithm should you use if you’re looking for faster performance and smaller key sizes compared to RSA?
AES
ECC (CORRECT ANSWER)
DES


Which asymmetric encryption algorithm is commonly used for digitally signing cryptocurrency transactions, such as in Bitcoin?
RSA
ECC
ECDSA (CORRECT ANSWER)
Sub-Unit 7
Quantum computers may render some encryption algorithms obsolete as they can factorize numbers very efficiently thus being able to break some algorithms. 
TRUE (CORRECT ANSWER)
FALSE





