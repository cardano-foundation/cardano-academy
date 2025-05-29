**Aiken (2023)**

Developers with a preference for imperative programming languages will be relieved to know Plutus Core, or UPLC, is an easy compilation target for most functional programming languages. The standard features of such languages like immutable data structures and higher-order functions are a good match for Cardano's eUTxO ledger model, where UTxOs are immutable.  

**Figure 49**: Aiken UPLC

As mentioned, Haskell code running on the Plutus Platform compiles to UPLC, and each Cardano node includes a UPLC evaluator, which is a CEK machine. The compiler is the crucial component here as it allows developers to use their preferred high level language, which also translates, or compiles, to the same UPLC machine language understood by the Cardano ledger. 

**Figure 50**: Overview drawing from @ktorz

Aiken has its own compiler tailored for writing validators on Cardano, so it feeds back relevant and informative error messaging and diagnostics. Aiken’s Language Server Protocol (LSP) integrates with popular editors like *VSCode*, *Zed* and *Neovim* and enables auto-formatting, code completion and syntax highlighting. Naturally, readability and auditing are easier as a result. 

**Figure 51**: Aiken hello_world.ak 

There is now a choice of high-level languages that compile to UPLC, none of which depend on Haskell. To date, Aiken has gained the most developer adoption and is the preferred choice for writing smart contracts, or validators, on Cardano. 

Named after the mathematician Howard Aiken, it is a functional domain-specific language (DSL) written in Rust and released under an open source licence. Unlike Haskell, it is built specifically with the Cardano blockchain in mind. It boasts a smooth developer experience and comes with state-of-the-art tooling, taking inspiration from modern programming languages like *Rust*, *Elm* and *Gleam*. 

With an open source ethos from the beginning, Aiken began with conversations between developers Kasey White and Lucas Rosa. It quickly attracted many other dedicated contributors, as well as support from *TxPipe*, who have hosted the busy discord server since. The Cardano Foundation was also quick to see Aiken’s potential and has supported the project with engineering resources. Aiken is hosted by PRAGMA, a member-based, not-for-profit open-source association for blockchain software projects. 

Aiken describes itself as 'The modern smart contract platform for Cardano,' but what does this mean? While Haskell has been around since the 1990s, and Plutus since 2018, Aiken had its alpha release in September 2024 but was widely adopted by projects even before then. It is a brand new language with its own C-family syntax, but it's still a functional programming language with static typing, type inference, and without any unintended side effects. Its compiler is written in Rust, and everything was designed in such a way that you can reuse the Rust libraries for other low-level tasks. 

Aiken has a fully working version of this virtual machine we spoke of earlier, except it’s written in Rust. Again, there is room for confusion, as you will see the Plutus virtual machine mentioned mostly in documentation. Think of it as there being two implementations, two different virtual machines, with each acting as a UPLC interpreter in practice. 

This is an important point. Sometimes it is said *'Haskell is more secure than Aiken'* but this is a misnomer. They both run on virtual machines in the Cardano ledger, benefiting from the same security stemming from the same execution model. There is no magic shield against exploits and attacks. Just as anyone can flush their passphrase down the toilet, any developer can write insecure code in Haskell or Aiken. 

**Figure 52**: Aiken Virtual Machine (written in Rust)

Aiken is a lean language which aims to free itself from unnecessary features and instead provide a comprehensive, opinionated solution with minimal configuration needed. Everything works out-of-the-box and with language-wide standards enforced by the compiler. Developers have remarked how Aiken is easy to learn and getting started takes just a few minutes. Aiken adopts a keep-it-simple approach. Compared to other languages, Aiken scripts, by design, do not support as many features as general purpose Turing-complete languages. Aiken is not a high-level general-purpose language. It is compact, designed meticulously to produce small, efficient scripts for on-chain Cardano smart contracts that integrate with most languages off-chain. As @KtorZ explained on Discord:[^1]

*The whole rationale behind 'keeping things simple' is to*: 
  - *(a) Avoid people writing too complicated code and shooting themselves in the foot. It's a smart-contract, you want to keep it simple and intelligible.*
  - *(b) It makes it easier to then build static analysis tools and the like on top. The smaller the language, the easier you can build these kind of useful addons.*

Aiken has garnered praise from developers for its Rust-like syntax that retains the strengths of Haskell, as a functional language in its own right. Many projects have reported substantial performance gains with faster and more efficient smart contracts. Aiken’s thoughtful design supports blueprint stub generation, which are effectively templates for different programming languages, and this facilitates an effortless integration between Aiken and off-chain components. 

While Aiken’s focus is enabling lean on-chain validators, it also facilitates off-chain interoperability. It promotes compatibility with DApp’s off-chain components and third party tooling. This philosophy allows you to move most of a DApp's architecture off-chain. 

A contract blueprint enables communication between on-chain code and off-chain code written in different languages. These blueprint stubs can be used as templates encouraging interoperability with other languages and ecosystems. CIP-57 outlines the full specification of a contract blueprint. 

Many developers had not found the Plutus platform a seamless match for using other languages off-chain. Despite issues with configuration and troubleshooting, many projects persisted with their favourite languages off-chain. For these teams who wish to work with their preferred tools and languages for off-chain code, Aiken’s blueprint stubs make life much easier. For example, the Java Cardano Client Lib supports Java class generation[^2] by Aiken blueprint annotations. According to the State of the *Cardano Developer Ecosystem 2024 survey*,[^3] Typescript, Javascript and Rust are the preferred languages for off-chain code. 

[^1]: Aiken Roadmap, discord.com/channels/946071061567529010/1068227395900952606/1068252286217900173
[^2]: Java Cardano Client Lib supports Java class generation# by Aiken blueprint annotations, x.com/satran004/status/1813604307360760143
[^3]: State of the Cardano Developer Ecosystem 2024, cardano-foundation.github.io/state-of-the-developer-ecosystem/2024/#what-language-s-do-you-use-or-plan-to-use-for-writing-off-chain-code
