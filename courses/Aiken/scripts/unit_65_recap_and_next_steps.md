# Recap and next steps

Phew! ...so that’s it. We covered a lot, tracking the evolution of account models and smart contracts on Bitcoin and Ethereum. We looked back at the early days of programmability on Cardano with Haskell, and how a host of high-level programming languages now also compile to Plutus Core. We focussed on the most popular option, Aiken, which has greatly improved the developer experience on Cardano while maintaining the benefits of a functional programming language. 

That said, we’ve only given you a taste of what Aiken can do. We haven’t covered more complex concepts like backpassing, upcasting and downcasting, and there are more advanced patterns to study. There is much more to come from the Aiken team no doubt, as Zero Knowledge proofs and on-chain governance features were only recently introduced on Cardano. Hopefully, we have whet your appetite to continue learning more about Aiken.  

## Next steps
For next steps, you should work through the 'Getting Started' checklist[^1] from the Aiken documentation. We alluded earlier that most of your DApp will reside off-chain. Mesh.js and Lucid Evolution are just two examples of the more popular frameworks for creating Cardano transactions and off-chain code. You can find more at the Cardano Developer Portal.[^2] 

There are plenty of hands-on courses that should form part of your study list:

- Aiken documentation: aiken-lang.org 
- The Evolution of Aiken - From Alpha to General Availability blog[^3] by KtorZ
- Rhys from STOIC Pool produced a video series[^4] about Aiken on the Cardano Community channel.
- Andamio.io  host a Project-based learning Aiken course
- IOG Plutus Pioneer Program v4 contracts have been translated to Aiken[^5]
- For more technical people, an understanding of UPLC will make life easier for you. The complete syntax for Untyped Plutus Core comes from the original Formal Specification of the *Plutus Core Language*.[^6]
- In terms of troubleshooting tools, the Aiken interpreter helps as best it can, for example, by raising errors when encountering a type mismatch. There are also a growing number of tools provided by the ecosystem, one of which is Gastronomy, which makes the link between your Aiken program and its final UPLC form. So when you look at some UPLC node, you can actually tell which part of your Aiken program it corresponds to, and walk step-by-step through the execution. Delicious!
- Awesome Aiken[^7] lists libraries, DApps, Projects and Tutorials of note from the ecosystem. 
- You should also bookmark a *GitHub search*[^8] for any projects using Aiken to see the latest content.
- Keep an eye on what’s been released in the ChangeLog[^9] and track what’s coming in the Project Tracker.[^10] 
- For support, you can talk directly to the Aiken team on their Discord. 
- *elm-cardano*[^11] is an Elm offchain package for Cardano. This project aims to be the friendliest and most productive way of handling an off-chain Cardano frontend. It should be a perfect match to Aiken for on-chain code. 
- *Rosetta Smart Contracts*[^12] is a GitHub repo which hosts a chrestomathy of smart contracts, including implementations of use cases in different smart contract languages. Details on the comparison between different smart contract languages are available in the research paper *Smart Contract Languages: a comparative analysis*[^13] 

## Food for thought
It’s in this research paper, where the Italian authors ask…

  *An open question is whether it is possible to reconcile the procedural style with the UTXO-based model, so to program smart contracts à la     
   Solidity while preserving the key strengths of UTxO blockchains like Cardano (e.g., the absence of transaction-ordering dependencies and the 
   parallelizability of transactions).*

While it is perhaps too early to say definitively if Aiken has achieved this just yet, it has made great strides[^14 considering General Availability was September 2024. Watch this space as this still fledging ecosystem may soon answer an emphatic 'yes' to the above question. 

[^1]: Aiken-lang.org checklist, aiken-lang.org/fundamentals/getting-started
[^2]: Cardano Developer Portal, developers.cardano.org/Cardano Developer Portal, developers.cardano.org/
[^3]: The Evolution of Aiken, pragma.io/blog/2024-09-04-aiken-from-alpha-to-general-availability/
[^4]: Cardano Smart Contracts - Aiken Language, Video series by STOIC Pool Aiken, youtube.com/playlist?list=PLCuyQuWCJVQ1Zz9ySRMH_J6EymxhnZ0Hu
[^5]: IOG Aiken validators, github.com/input-output-hk/plutus-pioneer-program/tree/aiken-fourth-iteration
[^6]: Plutus Core Specification, aiken-lang.org/resources/plutus-core-specification.pdf
[^7]: Awesome Aiken, github.com/aiken-lang/awesome-aiken
[^8]: Latest Aiken content on GitHub, github.com/search?q=aiken&type=repositories&s=updated&o=desc
[^9]: Aiken changelog, github.com/aiken-lang/aiken/blob/main/CHANGELOG.md#changelog
[^10]: Aiken Project Tracker, github.com/orgs/aiken-lang/projects/2/views/1
[^11]: elm-cardano, github.com/mpizenberg/elm-cardano
[^12]: Rosetta smart contracts, github.com/blockchain-unica/rosetta-smart-contracts
[^13]: Smart Contract Languages: a comparative analysis, arxiv.org/abs/2404.04129
[^14]: Aiken General Availability announcement, x.com/aiken_eng/status/1831083156272984507
