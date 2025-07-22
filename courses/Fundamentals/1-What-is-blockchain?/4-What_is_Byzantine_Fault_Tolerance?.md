**What is Byzantine Fault Tolerance?**

Banking and traditional payment systems are built on ‘trusting’ a central entity. Cryptocurrencies offer an alternative, running on top of ‘trustless’ blockchain technology. Just like any payments system, users of a cryptocurrency network also need to agree on the current state of the blockchain. They must reach ‘consensus’, but achieving consensus in a distributed system securely and efficiently is not a trivial feat. 

How can a distributed network of participants agree on a course of action if we know there are some bad actors behaving dishonestly? This is the challenge posed by the thought experiment described in a 1982 paper known as the Byzantine Generals Problem. 

The conundrum is about Byzantine generals attacking a walled city who face communication problems when trying to agree on their next move. Each general has his own army, and each army is deployed in different locations surrounding the target city. The generals need to decide together whether to attack or retreat. It is impossible to know in advance which is the right option, but their chances will be much better if they reach consensus, and move forward in a coordinated manner. Note that:

1) each general must vote to attack or retreat 
2) votes are irreversible
3) all generals must agree to the same decision 

The generals can only communicate through messages which may not make it to all other generals, could be misinterpreted, or misspoken along the way. Assuming they reach the intended recipient, any of the other generals may still go rogue. 

If we apply the same dilemma to computer science, specifically blockchains, you can think of each general as a node, or a peer, on the network, and the nodes need to achieve consensus on the current state of the system. The majority of nodes in a distributed network must agree and execute the same action in order to avoid catastrophic failure.

This is where the property *Byzantine Fault Tolerance* comes from. If a system is described as Byzantine Fault Tolerant (BFT), it is robust enough to achieve consensus in adverse conditions. It will continue functioning even if some of its nodes stop communicating or act maliciously. 

Different blockchains use various consensus algorithms to achieve Byzantine Fault Tolerance. The most common ones are Proof of Work (PoW) and Proof of Stake (PoS), but there are others too.

Byzantine fault-tolerant systems feature in many industries such as aviation, nuclear energy and the aerospace industry. Bitcoin was the first cryptocurrency to feature this unique property and leads us nicely into our next lesson…
