Plutus and Marlowe were the main programming languages for Cardano in the early years:

Plutus is a platform providing the supporting infrastructure and tools for writing smart contracts in Haskell. ‘Plutus’ and ‘Haskell’ are often used interchangeably. If you hear someone saying ‘it's coded in Plutus’, they really mean they are coding in Haskell using the Plutus Framework. To be specific, the Plutus Framework enables developers to create dApps which interact with a distributed ledger featuring scripting capabilities. It’s not just a language, it’s an entire platform that supports dApp development in its entirety, end-to-end from writing scripts, to testing, runtime support, and verification. 

Plutus is a platform made of 3 main components: 

- Untyped Plutus Core (UPLC) is the 'machine code' for the Cardano ledger
- PlutusTx is a plugin for compiling Haskell into UPLC to form the on-chain component. 
- Plutus Application Framework is the collection of tools for writing smart contracts in Haskell

It is said that to become a proficient developer on Cardano, one must understand three key concepts:

- The Extended Unspent Transaction Output (eUTXO) model
- On-chain code, Plutus Core, which runs on the blockchain 
- Off-chain code which runs on the user’s device. 

Marlowe is a simple programming language for writing financial smart contracts for Cardano. It is named after the Elizabethan poet, dramatist and spy, Christopher Marlowe. Marlowe is limited to financial applications and is not Turing-complete. It is DSL (Domain specific language) for people who are experts in finance rather than programming. You can code in Marlowe directly, or also utilize Blockly, a visual programming tool that allows you to design contracts by dragging and dropping connecting blocks that represent the various components.

It’s important to emphasise that you do not need to know Haskell to write smart contracts on Cardano. Let’s zoom out for a moment, to understand the bigger picture. As we mentioned, Haskell programs, coded on the Plutus Platform, compile to Untyped Plutus Core (UPLC) and while the Cardano ledger only understands Plutus Core, this low-level machine language is not something developers code in day to day. You can choose from a growing list of high-level languages which compile to UPLC.  

Developers crave flexibility to use their favourite language for what is typically the largest part of their dApp, the off-chain component. So although Cardano is implemented in Haskell, it is UPLC that is actually executed. There is no dependency or reliance on Haskell. Other languages can compile to UPLC too. One of those is Aiken. 

Named after the mathematician Howard Aiken, it is a functional domain-specific language (DSL) written in Rust and released under an open source licence. Unlike Haskell, it is built specifically with the Cardano blockchain in mind. It places an emphasis on the developer experience and comes with ‘batteries included’ state-of-the-art tooling, taking inspiration from modern programming languages like Rust, Elm and Gleam. 

Aiken is a lean language which aims to free itself from unnecessary features and instead provide a comprehensive opinionated solution with minimal configuration needed. Everything works out-of-the-box and with language-wide standards enforced by the compiler. Developers have remarked how Aiken is easy to learn and getting started takes just a few minutes. Aiken adopts a ‘keep it simple’ approach. Compared to other languages, Aiken scripts, by design, do not support as many features as general purpose Turing-complete languages. Aiken is a small language, not a high-level general-purpose language, designed meticulously to produce small, efficient scripts for on-chain Cardano smart contracts that integrate with most languages off-chain. ‘Aiken users exhibit a tendency for Rust in off-chain scenarios’ according to the findings of the State of the Cardano Developer Ecosystem 2023 survey. 

Aiken has garnered praise from developers for its Rust-like syntax which retains the strengths of Haskell, as a functional language in its own right. Many developers have reported substantial performance gains with faster, more efficient smart contracts. Aiken’s thoughtful design supports blueprint stub generation, which are effectively templates for different programming languages, facilitating an effortless integration between Aiken and off-chain components.

There are other programming options we should mention:

Helios is another Domain Specific Language (DSL) that compiles to Plutus-Core. It is a new language built from the ground up with Cardano in mind. Helios is also a functional language but is very similar to TypeScript. 

OpShin is an implementation of Cardano smart contracts written in a strict subset of Python. It enables you to write smart contracts in completely valid, albeit restricted Python3. 

Plutarch is a typed eDSL (embedded domain specific language) in Haskell for writing efficient Plutus Core validators. It is not a new language, it’s just good old Haskell with no restrictions. 

plu-ts is a library to enable Cardano-related software to be written entirely in TypeScript. 

Scalus is a Scala implementation of Plutus. 

Unlike many blockchains who adopt a ‘move fast and break things’ approach, Cardano has always stuck to a deliberate, careful and methodical strategy. Despite this relative conservatism, Cardano’s GitHub repositories have been very active in 2021, 2022 and again in 2023. 

As adoption grows, there are more and more options for newcomers. Acknowledging that Java is still the preferred language for many enterprise developers, the Cardano Foundation has written various tools and services in Java, and released them under an open source licence to encourage collaborations and community contributions. For example, the Identity Wallet is a W3C-compatible mobile wallet for managing self-sovereign identities across Cardano and other blockchains. The wallet supports multiple standards, integrating key event receipt infrastructure (KERI) for interoperability so as to fit a broad range of use cases and foster enterprise adoption.
