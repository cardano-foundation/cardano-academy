We spoke a bit about scripts, also referred to as smart contracts…. But from now on we’ll refer to them as validators, as they act like predicates, or pure functions always returning either **True** or **False**. Validators are fully deterministic, as their execution depends only on the transaction they're involved with. So we know a transaction's outcome before sending it to the network.

We introduced **datums** already as a free payload that can be attached to script execution. However, we need a few more ingredients to express some validation logic, capture state and state transition. Another new component that comes with eUTxO is the **redeemer**. 

The redeemer is some data that accompanies the transaction at script execution. This could represent the bill before you pay with your vouchers. The datum could be the original order. i.e. provided along with the order taken by the waiter to the kitchen. People often explain the redeemer as the 'key' that 'unlocks' the input, similar to how a digital signature unlocks output at a PubKey address. The spender of a transaction usually submits the redeemer as a script input.  

**Figure 29:** Plutus Virtual Machine 

In programming speak, datums are equivalent to local states, while redeemers act as user inputs provided in the transaction itself. For mathematicians, you can think of datums as being a function’s parameters, while redeemers are like its arguments.

To recap, when a script is run for validation, it optionally receives a datum, redeemer and also a context as arguments. The **context** consists of the transaction being validated along with all the transaction inputs and outputs. In addition to the hashed public keys we had before at an address, the eUTxO model enables addresses to contain hashed **scripts**, written in a programming language that compiles to *Plutus Core*. 

