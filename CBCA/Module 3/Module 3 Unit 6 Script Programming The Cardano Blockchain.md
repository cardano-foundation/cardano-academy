# Unit 6 - Programming The Cardano Blockchain

## Learning Objective
By the end of this unit, the learner should be able to:
- Gain a high-level understanding of what a ‘Virtual Machine’ is
- Understand what  compilers are and how they work 
- Understand what  Plutus Core is
- Understand  the memory and steps execution costs 
- Describe a few programming languages available on Cardano
- Enumerate the pros and cons of each

## Introduction
Hello everyone, and welcome back for another topic. My name is [speaker name] and thank you for joining me today. 

## Table of Contents
It's impossible to talk about Blockchain without talking about Smart contracts. Programmable ledgers enable automating a whole class of financial operations in a completely new execution model. In previous units, we have explored many related topics. We've seen the differences between the account model and the extended UTxO model. We have also seen the kind of architecture decentralized applications operate in. We mentioned smart contracts and on-chain logic back then, but didn't explore further. That time has finally come.

## Fundamentals

### About Programming Languages
Let's start our journey by talking about programming languages. What is a programming language? What is it for? At a very high level, a programming language is nothing more than a set of instructions for a computer to execute. It is a specification of a task to perform. A specification can take various forms. Even just an instruction given orally can serve as a specification. A law text is also a form of specification. A specification is always written with an audience in mind. Said differently, you need someone to interpret that specification in a specific situation. Lawyers, for example, spend their time interpreting the law.

What sets a programming language apart is how the specification has to be unambiguous.  More importantly, it has to be interpreted by machines. And we can see how our natural language is unfit for that purpose. Even with the recent progress in large language models, human speech still makes for an impractical specification language. This is even more true when the recipient is a computer. At the end of the day, a computer is a set of transistors and electronic components that only understand binary instructions resulting from an electric signal. A programming language is thus something that sits between us humans and the machine as a means of communication.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.1.png)

There exist multiple levels of programming languages. Some are more expressive than others and almost feel like a natural language, whereas some are very close to machine language. Programming languages are typically said to be ‘low-level’ or ‘high-level’. What low and high levels truly mean depends on the domain. Most programmers or software engineers usually consider the C language a low-level programming language. Yet it's a pretty high-level language for microcontroller manufacturers.

Similarly, Haskell is often seen as one of the highest-level programming languages, but it's a low-level language for type theorists, computer scientists and mathematicians. All-in-all, it's a spectrum. The 'low' or 'high' qualifiers usually refer to the number of abstraction layers between the language and the underlying machine running it.

### About Compilers
Besides, programming languages are only one side of the story. To be executed, they need to be turned into machine code. Tools that perform this task are called compilers. A compiler is thus a program that turns a programming language into another, lower-level programming language. This process usually happens in steps because the higher the language, the harder it is to translate it to machine-readable instructions directly. A common practice is, therefore, to use intermediate representations or lower-level languages as compilation targets. For example, a programming language like Haskell will compile down to C, which in turn will compile to Assembly language, which directly maps into binary instructions for electronic components. It would be quite a stretch to go from Haskell to machine instructions.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.2.png)

Assembly languages are exciting because they are so low-level in the stack that they feel like talking to the machine directly. In fact, that is precisely what they are about. Consequently, there's not one assembly language but multiple as they depend on the final hardware components. Most commercial machines today fall into two categories: Intel x86 and ARM. We won't go into detail here, but keep in mind that machine code doesn't necessarily refer to one thing. There are, in fact, many more machine architectures than the two mainstream ones which can be found across the industry.

### About Virtual Machines
We have one more component to discuss - virtual machines. Let's recap first. Programming languages are means of writing unambiguous instructions to a machine. They are turned into machine code by a compiler. Computers can comprehend machine code and perform tasks accordingly. Great! But it would be too easy if it stopped here. While all programs are eventually executed by a computer, there are scenarios where we need a different execution model. For example, what if you wrote a program for a specific machine architecture that runs on an aircraft flight system but you wanted to avoid running an actual aircraft to test your program? In this scenario, you'd prefer being able to run your aircraft program as if you were running it on the aircraft.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.3.png)

Virtual machines were invented to solve that kind of problem. A virtual machine is an execution environment that mimics a specific hardware architecture. It provides the same capabilities and interfaces that the real architecture would have. Said differently, it's a program that behaves as if it were a computer, with hardware components, peripherals, etc.. One notable trait of virtual machines is how they can emulate an architecture that doesn't exist in the real world. For example, you could build the perfect computer as a virtual machine or a computer which ignores all instructions between 11:00 p.m. and 6:00 a.m. Or, more realistically, you could design a virtual machine for running smart contracts in a completely controlled environment.

## Programming on Cardano
### Untyped Plutus Core
You have undoubtedly heard of the Ethereum Virtual Machine (known as EVM) or the Plutus Virtual Machine (known as Plutus VM). Smart contracts aren't executed like any other program on your computer. There's no reason for a smart contract to access your computer's CPU directly or to write data to your computer's RAM. On the contrary, there are excellent reasons not to grant this kind of power to a smart contract. Virtual machines provide a safe execution environment for smart contracts, with safeguards and specific capabilities. In particular, blockchain virtual machines must have one crucial property: they need to be able to quantify resource usage with a high degree of precision.

Running a program on your laptop takes resources, whether it is processing power, memory or disk space. Yet, because hundreds of other programs are running simultaneously, it is hard to isolate the precise cost in resources of one specific program. It's also difficult to completely prevent that specific program from interfering with the execution of another program. Virtual machines provide a nice interface that sits between any other program and the actual machine, emulating another machine's architecture. They can intercept every step of another program execution and respond as if those steps had been executed via a specific set of hardware components. They are like machines, after all!

Cardano is no different. The Cardano ledger embeds a virtual machine capable of specific operations to execute smart contracts in isolation. Like any other virtual machine, it provides built-in instructions and operations that programs can rely on. For example, the machine knows how to calculate a SHA-256 hash digest, which is commonly calculated in a contract. The virtual machine also knows a bit of programming. For example, it knows basic arithmetic operations and how to calculate function results. In the case of Cardano, the virtual machine's machine code is called 'Untyped Plutus Core', or UPLC for short. UPLC is a polymorphic lambda calculus with added built-ins. A lambda calculus is one way of representing computations, particularly well suited for mathematical logic. Polymorphic relates to the ability of functions to be written with generic type arguments. Other commonly known computation models may include Turing machines, on top of which most modern computers are built, or Finite State Machines, which are often used to power simple automatons such as vending machines.

### Plutus
A common misconception is that the Cardano ledger executes Haskell programs. It does not, at least not directly. The ledger only comprehends Plutus Core, and given that this is as low as one can go on that virtual machine, it isn't generally something written by hand. Instead, Cardano provides several higher-level programming languages that compile down to UPLC. Haskell is one of them. Aiken is another popular option. If you're familiar with the Cardano ecosystem, you have certainly seen or heard about Plutus. So, what exactly is Plutus?

A second common misconception is that people have a tendency to say  'Plutus' when they genuinely mean 'Haskell'. Officially, Plutus refers to the programming platform which encompasses different elements:

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.4.png)

- (Untyped) Plutus Core: It is the 'machine code' for the Cardano ledger that we just talked about;
- Plutus Tx, which is a plugin for the mainstream Haskell compiler which allows turning a subset of Haskell into UPLC;
- Plutus Application Framework: a collection of tools for working with smart contracts in Haskell.

Although nowadays, 'Plutus' is more commonly used to refer to the low-level on-chain language. So Plutus, Plutus Core, Untyped Plutus Core and UPLC are more-or-less synonymous. This terminology is indeed a little confusing! 

### Memory and Steps
One particularity of the Plutus VM is how it measures costs along two dimensions: steps and memory. Each instruction in Plutus has a specific cost associated with it. Some operations have a fixed cost, and some depend on their operands. For example, computing the result of an arithmetic multiplication depends on how large the numbers are. The execution cost is, therefore, quantified in terms of the number of steps the virtual machine needs, to find the result, and the quantity of memory it requires. Some operations demand to store intermediate results temporarily and will cost a little more than others.

These costs are entirely configurable and are captured in a "cost model". This is nothing more than a mapping between all the possible operations on the virtual machine and their associated cost. There's a cost model associated with each version of Plutus, and the actual configuration is stored as part of the protocol parameters. So they can be adjusted over time if needed. Hence, it is possible to know with extreme precision the cost of execution of any Plutus program.

The virtual machine can also interrupt the execution halfway if a program exceeds its authorized budget. Yet fortunately, programmers can utilize the virtual machine to simulate executions of smart contracts on their own development environment in the very conditions that the ledger would. As we've seen when we covered the extended UTxO model, the execution solely depends on the transaction that carries the script. There's no global state. In addition, the Plutus virtual machine is entirely deterministic: two executions of the same programs will not only give the same result; they will take the exact same number of execution steps and memory. 

This model gives programmers a fully deterministic and reproducible environment to work with. In the programming world, this is a big deal.

## Smart Contract Languages
Okay, enough talking about the internals and low-level details. These are necessary pieces of information to visualize how the machinery works. Yet, it's not something people deal with daily -- unless they are compiler engineers. When writing programs, programmers tend to prefer high-level languages as they can easily capture business requirements and are easier to audit. As we hinted at earlier, Cardano has many flavors regarding smart contract programming languages. So, let's explore some of the most notable efforts and talk about their commonalities and key differences.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.5.png)

### Haskell
Haskell is the most famous option on Cardano for being the first one available. It has been pushed from the start through efforts like the Plutus Pioneer Program, which teaches Haskell for most parts. It is a natural first choice when it comes to Cardano since the rest of Cardano is also implemented in Haskell -- yet it's not the only reason that makes it a good choice. Haskell is a functional programming language with strong static typing and high expressiveness. These are all qualities we look for in modern languages as they help reduce common mistakes and ease the translation of complex requirements into programs.

We already discussed in earlier units how Haskell is a particularly relevant choice for building critical applications due to its proximity to mathematics and formal methods. This argument also applies to the Haskell toolchain for Cardano. There are, however, a few notable differences between Haskell, which runs on your computer, and Haskell, which runs on the Cardano blockchain through the Plutus virtual machine.

Remember that the Cardano ledger only understands Plutus core, not Haskell. This means that Haskell has to be compiled into Plutus core. The execution environment is also somewhat different. When running on one's laptop, compiled Haskell will eventually be translated into machine code for Intel or ARM hardware. On Cardano, the Plutus virtual machine executes the compiled Haskell, and program behaviors aren't always identical to mainstream machine code.

And because of this different execution model, the ecosystem of functions and libraries normally available to Haskell developers is also restricted. Indeed, programmers often reuse code from others. Code that solves specific generic problems is often packaged into libraries and shared to benefit others. Each programming language, therefore, comes with a rich ecosystem of reusable libraries fit for purpose. Code libraries allow each and everyone to build more complex, bigger programs faster. When a program is compiled, it usually embeds many of the libraries it relies on. So, while programmers may write only a few hundred lines of code, a final program may include much more.

However, the space is limited on the blockchain, specifically in transactions carrying scripts. It is challenging or simply infeasible to include many such code dependencies. Thus, in practice, programming in Haskell for Cardano and programming standard Haskell are vastly different experiences. Only a fraction of the Haskell ecosystem can be leveraged, mainly by borrowing from the syntax and existing tooling. Note that these limitations aren't specific to Haskell. They stem from the different execution model imposed by the ledger and would be true of any mainstream language.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.6.png)<br>
![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.7.png)<br>
![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.8.png)<br>

### Aiken
This is a perfect segway into another popular solution on Cardano: Aiken. Like Haskell, Aiken is a functional programming language with strong static typing. So what's the difference? Unlike Haskell, Aiken is built specifically for the Cardano blockchain and focuses on the developer experience. It is inspired by modern programming languages and comes with state-of-the-art tooling.

In contrast, Haskell is a relatively old language with pros and cons. Being there for a while, it has a robust compiler and a well-furnished ecosystem. On the other hand, some tools are outdated, and the language itself can feel cluttered with legacy features. Plus, being a general-purpose language, it comes with functionalities that aren't useful in a blockchain environment.

Aiken trims these unnecessary features to provide an all-in-one opinionated solution with a zero-configuration policy. Everything should work out of the box and with language-wide standards enforced by the compiler. Aiken focuses on improving the developer experience by being easy to learn and get started with. Behind the scenes, Aiken also uses a slightly different execution model than the Haskell to Plutus Core compiler. While they both ultimately rely on Plutus Core, they choose to represent and manipulate data differently, leading to different trade-offs regarding execution costs.

### Helios
Akin to Aiken, Helios is a Cardano-specific programming language born around the same time as Aiken. Like Aiken and Haskell, Helios is a purely functional language whose syntax is inspired by TypeScript. The main particularity about Helios is how it is a wholly siloed ecosystem. Indeed, the Helios compiler is written from scratch with no external dependencies to any library. This approach allows Helios to keep fine control of everything revolving around their ecosystem.

Not relying on any other code library also means that every bit of the language and tooling has to be re-implemented from the ground up. This is a double-edged sword as it gives control and freedom to various design choices, but it slows down the overall development of the ecosystem.

Like Aiken, Helios provides more than just a programming language; It comes with tools, software development kits and APIs to work with Helios from JavaScript. It is intended to be a solution easy to use for those building client applications solely in the browser.

### Embedded Domain Specific Languages (eDSL)
Full-blown programming languages like Haskell, Aiken or Helios are just some options available to smart contract developers on Cardano. Another class of tools falls in the category of embedded domain-specific languages, or eDSL in short. Those domain-specific languages are succinct programming languages written on top of an existing programming language. Think of them as pre-defined building blocks written in a specific language that will perform well-defined tasks.

eDSLs are usually good at solving simple problems of a specific scope. Programmers build them to put well-known words from their business domain onto more abstract programming tasks. This often eases the communication between engineering and business departments as they share one common vocabulary. For example, you often find eDSL for dealing with data stores, describing simple test scenarios or configuring software.

As it turns out, they are also great at representing smart contracts.

### Native Scripts
The first type of eDSL we find on Cardano is the so-called 'native script’, which was introduced during the Shelley era. Native scripts form a straightforward scripting language that allows the representation of multi-signature scenarios and simple time conditions. At present, the native script eDSL provides six primitives:

- Signature: specifies that a valid signature from a given public key is expected.
- All: implies that a list of native scripts must all be satisfied.
- Any: implies that at least one native script from a list must be satisfied.
- N-of-M: a generalization of 'All' and 'Any', which lets you specify how many native scripts from a given list must be satisfied.
- After: implies that the script is only valid if executed after a given slot.
- Before: implies that the script is only valid if executed before a given slot.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.9.png)

The primitives 'All', 'Any' and 'N-of-M' allow you to compose native scripts. 'Signature', 'After' and 'Before' allow us to express terminal conditions. It's a rudimentary language that the ledger understands, yet potent in many situations. In particular, they have been used in the early days of Cardano as minting policies for non-fungible tokens.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.10.png)<br>
![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/3.6.11.png)

### Marlowe
Another excellent example of eDSL on Cardano is Marlowe. As the result of multiple years of research and effort, Marlowe is an eDSL specifically designed to represent a large variety of typical financial operations such as escrows, bonds, swaps, etc. Like native scripts, Marlowe also comes with six primitives that are limited in scope, although they have more elaborate logic than native scripts. Those primitives are Pay, Close, If, When, Let and Assert. As you can imagine, Marlowe can express more complex branching logic than a mere multi-signature using If and When.

Marlowe also comes baked in with various observables. Said differently, Marlowe can assert the values of various transaction elements. Still, it isn't a full-blown programming language like Haskell. Some programs cannot be written in Marlowe. In contrast, Haskell, Aiken or Helios are said to be Turing-Complete. Turing completeness means that they can be used to implement any possible program executable by a (Turing-)machine. Being Turing-complete has both pros and cons. Marlowe turns this into a strength. As Marlowe isn't Turing-Complete, only a fixed number of programs can be written in it. For a given transaction, it is actually possible to compute, test and verify every single Marlowe program that can be created from it. Consequently, it is theoretically possible to guarantee that a given Marlowe program has no security flaw and no exploit. This guarantee level is much harder to achieve with Turing-Complete programs, which are not necessarily guaranteed even to terminate!

## Review
This completes our unit about programming the Cardano blockchain. We've introduced the fundamentals of computability theory at a very high level. Enough to understand how the Cardano ledger runs a virtual machine to execute smart contracts. Then, we covered the most popular options for Cardano developers, distinguishing between Turing-complete languages and eDSL. And as we speak, even more solutions are being built and maturing. So, stay tuned and see you next time.

## References
[Ref.8.6.1] Type Theory & Functional Programming, Professor Simon Thompson, University of Kent, Available from:  https://www.cs.kent.ac.uk/people/staff/sjt/TTFP/ttfp.pdf/ , Accessed: 5 Oct 2023

## Glossary

- *Type System:* A type system is a logical framework made up of a set of rules that give each term—a word, phrase, or other group of symbols—an attribute termed a type (for instance, integer, floating point, or string).
- *Type Theory:* Type theory is the academic study of type systems, and a type theory is the formal presentation of a particular type system. One influential type theory is Alonzo Church's typed λ-calculus.
- *Machine code vs Assembly language:* Low-level programming languages used to create programs include machine language and assembly language. While assembly language is a representation of machine language that is comprehensible by humans, machine language is the binary code that computers comprehend and execute.
- *Polymorphic:* Polymorphism is the notion that you can access objects of different types through the same interface. In other words, you can have multiple implementations of the same abstract concept.
- *Lambda calculus:* Lambda calculus is a mathematical system used to describe mathematical functions and programs. It covers some of the key, universal characteristics of a wide range of programming languages.
- *Static typed languages:* A language is said to be statically-typed if the variable types are known at compile-time instead of at run-time. Compile time is when the programming code is converted to machine code. Runtime is the time when a program is running and usually occurs after compile time.

## Questions

**Sub-Unit 1**

*What do we call a programming language which is close to natural language and far from machine instructions?*
- Smart
- **High-level (CORRECT ANSWER)**
- Complex-level
- Turing-complete

*True or False, a program is a specification for a machine?*
- **True (CORRECT ANSWER)**
- False

*Select the correct statements about programming languages:*
- **At a very high level, a programming language is nothing more than a set of instructions for a computer to execute (CORRECT ANSWER)**
- **A programming language is something that sits between us humans and the machine as a means of communication (CORRECT ANSWER)**
- What sets a programming language apart is how the specification has to be interpreted by human speech
- There exists only one level of programming languages
- Most programmers usually consider the C language a high-level programming language

**Sub-Unit 2**

*Which statement gives a high-level definition of a 'Virtual Machine'?*
- A computer which only exists in the metaverse
- A program that runs in the cloud
- **It's a program that behaves as if it were a computer, with hardware components, peripherals, etc.. (CORRECT ANSWER)**
- A blockchain execution engine

*Which of the following statements is NOT true regarding virtual machines?*
- They can be used to precisely measure execution steps of a program
- They need real machine resources to run
- They are often used in the blockchain industry
- **They can only emulate hardware components that exist in the real world (CORRECT ANSWER)**

*Select the correct statements about virtual machines:*
- **A virtual machine is an execution environment that mimics a specific hardware architecture  (CORRECT ANSWER)**
- **It provides the same capabilities and interfaces that the real architecture would have  (CORRECT ANSWER)**
- It is a program that behaves as if it were separate from a computer, only making use of software components, etc
- One notable trait of virtual machines is how they cannot emulate an architecture that doesn't exist in the real world

**Sub-Unit 3**

*Which of the following statements are correct:*
- **Virtual machines provide a safe execution environment for smart contracts (CORRECT ANSWER)**
- Virtual machines create a very unsafe execution environment for smart contracts
- **Blockchain virtual machines need to be able to quantify resource usage with a high degree of precision (CORRECT ANSWER)**
- A virtual machine interface is not able to emulate another machine’s architecture

*What is executed by the Cardano ledger when evaluating smart contracts?*
- Haskell
- **Plutus Core (CORRECT ANSWER)**
- Assembly
- Solidity

*Select the correct statements:*
- The Cardano ledger directly executes Haskell programs
- **The Cardano ledger only comprehends Plutus Core (CORRECT ANSWER)**
- **Plutus refers to the programming platform which encompasses elements such as (Untyped) Plutus Core and Plutus Tx (CORRECT ANSWER)**
- **Plutus Application Framework: a collection of tools for working with smart contracts in Haskell (CORRECT ANSWER)**
- Cardano only provides one higher-level programming language that compile down to UPLC

**Sub-Unit 4**

*The Plutus virtual machine measures resource usage along two dimensions. What are they?*
- Steps and disk space
- Disk space and energy
- **Steps and memory (CORRECT ANSWER)**
- Memory and energy

*How does the virtual machine handle programs that exceed their authorized budget?*
- It terminates the program immediately
- It allows the program to continue execution
- **It interrupts the execution if a program exceeds its authorized budget (CORRECT ANSWER)**
- It increases the authorized budget for the program

*What can programmers do with the virtual machine in their own development environment?*
- They can only simulate executions of smart contracts
- They can't use the virtual machine for development
- **They can utilize the virtual machine to simulate executions of smart contracts on their own development environment in the very conditions that the ledger would. (CORRECT ANSWER)**
- They can only execute smart contracts on the main ledger

**Sub-Unit 5**

*Which of the following is NOT true regarding Haskell?*
- Haskell is a natural first choice for programmers, since the rest of Cardano is also implemented in Haskell 
- Haskell is a functional programming language with strong static typing and high expressiveness 
- **The Cardano ledger only understands Haskell (CORRECT ANSWER)**
- The Cardano ledger only understands Plutus core

*Which statement is NOT true about Aiken?*
- It is a pure functional programming language
- It is Turing-complete
- **It is complex to set up and configure (CORRECT ANSWER)**
- It compiles to Plutus Core

*What is one of the main characteristics of Helios, a Cardano-specific programming language?*
- It is a multi-paradigm language
- It is based on the Haskell programming language
- **It is a purely functional language inspired by TypeScript (CORRECT ANSWER)**
- It relies heavily on external code libraries

*What sets Helios apart in terms of its ecosystem?*
- It is built on top of the Haskell ecosystem
- **It is a wholly siloed ecosystem with no external dependencies to any library (CORRECT ANSWER)**
- It relies on numerous external code libraries

**Sub-Unit 6**

*What does 'eDSL' mean?*
- Extended Domain-Specific Language
- **Embedded Domain-Specific Language (CORRECT ANSWER)**
- Enabled Domain Specific Language
- Efficient Domain Specific Language

*What kind of trustless smart contract logic could you implement using a Cardano native script?*
- **A multi-signature between 3 participants, but only after a known date (CORRECT ANSWER)**
- An asset swap
- A token minting policy which ensures a maximum supply of tokens.
- A multi-signature between 2 participants, with different permissions for each signatory

*What are the six primitives that come with Marlowe?*
- Add, Subtract, Multiply, Divide, Equals, Not Equals
- **Pay, Close, If, When, Let, Assert (CORRECT ANSWER)**
- Create, Modify, Delete, Retrieve, Execute, Verify
- Input, Output, Loop, Break, Continue, Function

*How does Marlowe's level of Turing completeness compare to languages like Haskell, Aiken, and Helios?*
- Marlowe is Turing-Complete, just like Haskell, Aiken, and Helios
- Marlowe is more limited in its expressive power compared to Haskell, Aiken, and Helios
- **Marlowe is not Turing-Complete, while Haskell, Aiken, and Helios are (CORRECT ANSWER)**
- Marlowe is less secure but more versatile than Haskell, Aiken, and Helios
