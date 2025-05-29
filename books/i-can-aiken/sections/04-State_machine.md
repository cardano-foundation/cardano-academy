So the blockchain is essentially a state machine whose state updates as new blocks, full of transactions, are added. The scripting layer is where transactions are executed before they are bundled into blocks.

For cryptocurrency to be useful, we need to be able to transfer value. This transfer is done via a transaction, usually after some conditions defined in a smart contract are satisfied. Each smart contract language works hand in glove with an **accounting model** which keeps a record of who owns what. 

The two main accounting models are UTxO (Unspent Transaction Outputs)-based models and account-based models. While both models achieve a similar goal, they operate very differently. UTxO was introduced by Bitcoin, and the account-based model was subsequently introduced by Ethereum, then adopted by other mainstream blockchains such as Solana, Aptos, and Algorand. Cardano later extended the UTxO model, creating the extended UTxO model (eUTxO). You may be wondering why we didn’t mention the account model in the Cardano stack above. Which layer does it reside in? 

Before we give you our answer, understand that there is always some ambiguity about precise mappings to a suggested stack. Some models and protocols traverse, or impact, multiple layers. That said, if we were to place it, it would live somewhere between the settlement and consensus layers. eUTxO defines how the ledger state is represented and updated. It dictates how transactions are structured, validated, and how assets are owned and transferred. This is fundamental to the ledger's functionality. The eUTxO model also plays a crucial role in Cardano's consensus mechanism, Ouroboros. It enables efficient validation of transactions and ensures the integrity of the blockchain by preventing double-spending and other invalid state transitions.

**Figure 3:** Where the account model resides in the Cardano stack 

Cardano’s eUTxO model, as the name suggests, extends the capability of UTxO but also takes learnings from the account model. As we move through the timeline, you will gradually begin to see how everything is related and that all the pieces matter.

**Figure 4:** UTxO vs eUTxO 

Let’s take a step back in time to review each model and look at how each blockchain came to pass. Crypto’s origins stretch way back to the 1980s but we’ll begin our journey in 2008. We will focus on the milestones in black.
