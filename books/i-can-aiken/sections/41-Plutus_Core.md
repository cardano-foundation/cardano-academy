**Plutus Core**

UPLC, or Untyped Plutus Core, may be referred to as Plutus Core, or just Plutus. You will also hear of Plutus scripts, or Plutus validators, and they all refer to the same thing: UPLC programs that are run on-chain by all node-validating transactions. It can get confusing, however, as you will also hear of PlutusTx, now called Plinth, also referred to as Plutus scripts. Forewarned is forearmed!   

Every Cardano node has a built-in Plutus virtual machine, also written in Haskell, which provides basic instructions and operations that smart contracts need to execute securely. The machine code for this Plutus virtual machine is Plutus Core. So what exactly is Plutus Core at a basic level? 

Plutus Core is a Turing-complete, low-level language for smart contracts. It uses a polymorphic lambda calculus that allows functions to be written with generic type arguments. This flexibility, combined with its foundation in a well-researched computational model dating back to the 1930s, makes it a stable, powerful tool for building reliable and secure smart contracts. It also enables the creation of straightforward, formally verified tools for evaluating its code.

**Figure 44**: The Cardano blockchain stack 

**Memory and Steps**

A feature we touched on earlier was the Plutus VM’s execution model. Every task the VM completes requires some amount of resources, which come at a cost. The VM measures this by the number of steps the virtual machine requires, as well as the amount of memory it needs. 

The Plutus VM cost model maps all the possible operations the virtual machine is capable of with their associated cost. This is important because it is possible to predict precisely the execution cost for a Plutus script. 

You should recognise a repeated theme that resurfaces here again: the Plutus virtual machine inherits deterministic properties from the eUTxO model. Running the same scripts twice will return the same result, with identical number of executions steps and memory. Tweaking these scripts to complete more complex tasks will increase these costs proportionally, and you can compare the stats anytime by running a simple command such as **aiken check**

**Figure 45**: Ethereum global state

Ethereum’s non-deterministic gas model can give its users nasty surprises with large fees. By contrast, a script on Cardano requires that the resource budget, along with the fee required to cover it, is included with a transaction. The deterministic nature of eUTxO allows you to know both of these locally when constructing the transaction. The success of a script’s execution is binary, either **True** or **False**. The interpreter tracks resources for all script operations. If a transaction uses more resources than budgeted, the interpreter stops execution and returns **False**.  

**Figure 46**: Cardano state transition 

The Plutus Core version follows a standard notation scheme, with just two Plutus Core versions to date: 1.0.0 and the latest 1.1.0.
