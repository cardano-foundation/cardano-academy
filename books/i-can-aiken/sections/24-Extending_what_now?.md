Input Output Global’s research led to the development of the Extended UTxO model. This model addresses the challenge of combining expressive smart contracts with the simplicity of the UTxO model. Described in 2020 research papers, *The Extended UTxO Model*,[^1] and *Native Custom Tokens in the Extended UTxO Model*,[^2] it is a key component of Cardano's architecture and offers advantages in security and predictability. 

Cardano builds upon or extends the intuitive and elegant UTxO features we described earlier. In addition to inputs and outputs, it also includes elements that modify different parts of the blockchain state to enable stake delegation, governance votes and native assets. 

**Figure 24:**  Overview of a typical Cardano transaction

**Outputs**

On Cardano, a UTxO object represents these characteristics:
- A value representing the number of assets
- An address with the conditional logic for spending (delegating) those assets. This address defines ownership of the assets. 

There’s also a **datum**: an immutable piece of data linked with the UTxO and usually used to represent the state of a smart contract.

Cardano supports two types of assets: the main currency, ada, and user-defined native assets. Fungible and non-fungible tokens (NFTs) are both native assets treated as first class citizens. In other words, they have the same capabilities as ada in every sense, because the functionality is already built into the protocol. This reduces complexity for developers and opens up new uses. Cardano's native assets function based on a set of rules that govern the creation, issuance, and management of native tokens.  

**Figure 25:** Cardano native asset lifecycle  

**Inputs**

It’s a little counter intuitive, but think of an input as a reference to a previous output. Outputs are like vouchers with a unique serial number that refers to an input, or an old voucher consumed to make this new voucher. 

A transaction is like a restaurant order with instructions on which vouchers should be consumed and which new vouchers should be created in their place. It could be an order for anything. A voucher can be redeemed for a meal or used to pay the bill. The voucher represents a UTxO. For example, there must be as much voucher value in as there's voucher value out.  

An output that is not consumed, or spent yet, is called an **unspent transaction output**, or UTxO. The remaining orders, or UTxOs, on the kitchen wall defines the blockchain state.

An input's, or vouchers’s, serial number is the **hash digest** of the transaction that emitted the output, or old voucher it refers to. It is also the position of the output, or old voucher, within that older transaction. It may have been one of many outputs from a previous transaction. These two elements, the transaction id (TxId) and index (TxIx), make each input, or voucher, unique.  The outputs are removed from the available set, the UTxO set. Each UTxO can only be consumed once. Similarly, with our analogy, each voucher is torn up, or used, just once. 


[^1]: The Extended UTxO model, iohk.io/en/research/library/papers/the-extended-utxo-model/
[^2]: Native Custom Tokens in the Extended UTxO Model, iohk.io/en/research/library/papers/native-custom-tokens-in-the-extended-utxo-model/
