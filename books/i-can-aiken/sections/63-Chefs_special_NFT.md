# 63. Chef’s special NFT

This validator ensures that the 'Chef's Special' NFT is minted only once and only to the person who placed the original order for the specific dish. This creates a verifiable and secure way to manage the distribution of these unique NFTs.

```rust
use aiken/collection/dict.{to_pairs}
use aiken/collection/list
use cardano/assets.{PolicyId, tokens}
use cardano/transaction.{OutputReference, Transaction}
// The restaurant gives out a unique "Chef's Special" dish NFT to
// the first person who orders a specific meal of the day.

validator chefs_special_nft(order_ref: OutputReference, dish_name: ByteArray) {
 mint(_redeemer, policy_id: PolicyId, tx: Transaction) {

   // Get the transaction inputs and minted values (like checking the order and the NFT)
   let Transaction { inputs, mint, .. } = tx

   // Make sure only one "Chef's Special" NFT is minted
   expect [Pair(asset_name, amount)] = mint |> tokens(policy_id) |> to_pairs()

   // Check if the transaction includes the original order (order_ref)
   let is_order_placed =
     list.any(inputs, fn(input) { input.output_reference == order_ref })

   // Final checks (is the order placed, is only one NFT minted, and is the name correct?)
   is_order_placed? && (1 == amount)? && (asset_name == dish_name)?
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:
chefs_special_nft: This validator acts like a system for creating a unique 'Chef's Special' NFT. The validator ensures that the 'Chef's Special' NFT is minted only once, and only when the specific dish is ordered for the first time. The first customer to orders the special is rewarded with a unique NFT.
order_ref: This represents a specific customer's order, like their order number or receipt ID.
dish_name: This is the name of the special dish that triggers the NFT minting.

1. Importing Modules:
```rust
use aiken/collection/dict.{to_pairs}
use cardano/assets.{PolicyId, tokens}
Import necessary modules for working with lists, dictionaries, Cardano assets, and transactions.
aiken/collection/dict: Provides functions for working with dictionaries (key-value stores).
cardano/assets: Provides functions for working with Cardano assets, including NFTs (non-fungible tokens).
```

2. Validator Definition:
```rust
// The restaurant gives out a unique "Chef's Special" dish NFT to
// the first person who orders a specific meal of the day.
validator chefs_special_nft(order_ref: OutputReference, dish_name: ByteArray) {
…
}
```

This defines a validator named chefs_special_nft. 
order_ref: OutputReference: This is a parameter to the validator, representing a reference to the transaction output where the customer placed the order for the special dish.
dish_name: ByteArray: This is another parameter representing the name of the 'Chef's Special' dish as a byte array.

3. mint handler:
```rust
 mint(_redeemer, policy_id: PolicyId, tx: Transaction) {
…
 }
}
```

The mint handler deals with minting a new NFT using the associated policy.
_redeemer: This parameter is not used in the function (hence the underscore).

policy_id: PolicyId: This represents the ID of the NFT policy that governs the minting of the 'Chef's Special' NFT.
tx: Transaction: This represents the transaction that is attempting to mint the NFT.

4. Extracting Transaction Data:
```rust
   // Get the transaction inputs and minted values (like checking the order and the NFT)
   let Transaction { inputs, mint, .. } = tx 
```

This line extracts the inputs and mint fields from the tx object.
inputs is a list of transaction inputs, which are references to previous outputs being consumed in this transaction.
mint represents the minting of new tokens in this transaction.

5. Ensuring Only One NFT is Minted:
   // Make sure only one "Chef's Special" NFT is minted
   expect [Pair(asset_name, amount)] = mint |> tokens(policy_id) |> to_pairs()

This line ensures that only one 'Chef's Special' NFT is being minted in the transaction.
mint |> tokens(policy_id) extracts the tokens being minted under the given policy_id.
to_pairs() converts this into a list of pairs, where each pair contains the asset name and the amount being minted.
expect [Pair(asset_name, amount)] = … ensures that exactly one pair is present in the list, meaning only one type of NFT is being minted.

6. Checking for the Original Order:
   // Check if the transaction includes the original order (order_ref)
   let is_order_placed =
     list.any(inputs, fn(input) { input.output_reference == order_ref }) 
This line checks if the transaction includes the original order as one of its inputs.
list.any checks if any element in the inputs list satisfies the given condition.
The condition checks if the output_reference of the input matches the order_ref provided to the validator.

7. Final Validation Checks:
  // Final checks (is the order placed, is only one NFT minted, and is the name correct?)
   is_order_placed? && (1 == amount)? && (asset_name == dish_name)?
 }

This line performs the final validation checks:
is_order_placed?: Ensures that the order was indeed placed (by checking if the order_ref is present in the inputs).
(1 == amount)?: Ensures that only one NFT is being minted.
(asset_name == dish_name)?: Ensures that the name of the minted NFT matches the dish_name provided to the validator

8. Catch-All Condition:
 else(_) {
   fail
 }
}
This is a catch-all condition that handles any other scenarios, if the above didn’t return True
