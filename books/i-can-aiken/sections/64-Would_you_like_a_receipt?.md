# 64. Would you like a receipt?
If you don’t follow best practice when coding your validators, you are liable to fall foul of issues like UTxO contention. Contention occurs when multiple transactions attempt to spend the same UTxO. Naturally, only one transaction succeeds, while the others fail. Let's look at some ways we can avoid common anti-patterns.
We can write a validator in such a way that it mints a unique receipt for a transaction. This is done by ensuring the AssetName is a unique value specific to the transaction we are validating. Said differently, if we are to have only one receipt minted for every transaction, we can leverage blake2b_256 and cbor.serialise to arrive at a unique value that can be assigned to the AssetName. It does so by selecting the first input and concatenating its output reference and index to generate the expected token name.

This validator script ensures that:
Only minting transactions are allowed.
Only one type of token is minted per transaction.
The name of the minted token is derived from the first input's output_reference in a deterministic way.
Exactly one token with the calculated name is minted.

```rust
use aiken/builtin.{blake2b_256}
use aiken/cbor
use aiken/collection/dict
use aiken/collection/list
use cardano/assets.{PolicyId}
use cardano/transaction.{Transaction}
validator meal_order {
 // This validator expects a new order
 mint(_redeemer: Data, supplier_id: PolicyId, self: Transaction) { 
   let Transaction { inputs, mint, .. } = self
   // Check the first item on the order and combine its details to
   // generate the expected dish name
   expect Some(first_item) = list.at(inputs, 0)
   expect [Pair(dish_name, quantity)] =
     mint |> assets.tokens(supplier_id) |> dict.to_pairs()
   let expected_dish_name =
     first_item.output_reference
       |> cbor.serialise
       |> blake2b_256
   // Compare the dish name with the first order item reference
   and {
      dish_name == expected_dish_name,
      quantity == 1
      }
 }
 // The validator will fail if the transaction is not for placing an order.
 else(_) {
     fail
 }
}
```

## Explaining the code:

1. Importing Modules:
use aiken/builtin.{blake2b_256}: Imports the blake2b_256 function, a cryptographic hash function mostly used in Cardano.
use aiken/cbor: Imports the cbor module for encoding and decoding data in Concise Binary Object Representation (CBOR) format. This is a compact binary format commonly used in Cardano.

Cardano data structures frequently require serialization, and this is done with a structured binary format called CBOR, which is a binary data serialization format loosely based on JSON. Like JSON, it allows the transmission of data objects that contain name–value pairs, but in a more concise manner. This increases processing and transfer speeds at the cost of human-readability.

In the context of data storage, serialization is the process of translating data structures or object state into a format that can be stored or transmitted and reconstructed later. When the resulting series of bits is reread according to the serialization format, it can be used to create a semantically identical clone of the original object.

Concise data definition language (CDDL) is a specification meta-language for Concise Binary Object Representation (CBOR). Its main goal is to provide an easy and unambiguous way to express structures for protocol messages and data formats that use CBOR or JSON (JavaScript Object Notation). The Cardano ledger maintains a CDDL specification of all the Cardano objects

CBOR diagnostic allows for a user-friendly debugging experience as it’s more readable. Check out the Troubleshooting section of the docs for more detail. 

use aiken/collection/dict: Imports the dict module for working with dictionaries (key-value pairs).
use cardano/assets.{PolicyId}: Imports the PolicyId type, which represents the unique identifier of a token policy (a set of rules governing the minting of tokens).
use cardano/transaction.{Transaction}: Imports the Transaction type, which represents a transaction on the Cardano blockchain.
2. Defining the meal_order Validator:
validator meal_order { ... }: This defines a validator named meal_order. 


3. The mint Handler:
mint(_redeemer: Data, supplier_id: PolicyId, self: Transaction) { … }: This is the mint handler within the validator. It is executed when a transaction attempts to mint new tokens using this validator.
_redeemer: Data: This argument represents the redeemer, a piece of data provided by the user when interacting with the script. It's not used in this validator, hence the underscore.
supplier_id: PolicyId: This argument represents the policy ID of the tokens being minted. In our analogy, it's the ID of the restaurant.
self: Transaction: This argument represents the transaction itself being evaluated.

4. Inside the mint Handler:
let Transaction { inputs, mint, .. } = self: This line destructures the Transaction object (self) and extracts the inputs (list of UTxOs being consumed) and mint (information about the tokens being minted) fields.
expect Some(first_item) = list.at(inputs, 0): This line retrieves the first input from the list of inputs (inputs). The expect keyword ensures that the list is not empty; otherwise, the script fails.
expect [Pair(dish_name, quantity)] = mint |> assets.tokens(supplier_id) |> dict.to_pairs(): This line gets the tokens being minted with the given supplier_id, converts them into a list of key-value pairs (token name and quantity), and ensures there's only one token being minted.
let expected_dish_name =  first_item.output_reference |> cbor.serialise |> blake2b_256: This line calculates the expected name of the token (or 'dish' in our analogy). It takes the output_reference of the first input (a unique identifier), serializes it using CBOR, and then hashes it using blake2b_256 to create a unique token name.
dish_name == expected_dish_name, quantity == 1: This is the final validation condition. It checks if the actual dish_name (from the mint field) matches the calculated expected_dish_name and if the quantity of tokens being minted is exactly 1.

5. The else Clause:
else(_) { fail }: This clause ensures that the validator only allows minting transactions. Any other type of transaction will cause the script to fail.
