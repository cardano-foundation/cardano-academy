# 62. Stake at the restaurant

This validator effectively implements a system where:
Anyone can delegate ada to a stake pool.
Waiters can withdraw rewards (tips), but they must leave at least half of the ada in the stake pool for the restaurant.
This ensures a fair distribution of ada between the waiters and the restaurant.

```rust
use aiken/collection/list
use aiken/collection/pairs
use cardano/address.{Address, Credential}
use cardano/assets.{lovelace_of, merge, zero}
use cardano/transaction.{Transaction}
/// A restaurant has a stake pool where customers can delegate their ada to.
/// This validator manages the stake pool and ensures fair distribution.
validator stake_pool(restaurant_addr: Address) {
 /// Allow anyone to add ada to the stake pool. This is like a customer leaving a tip.
 publish(_redeemer, _certificate, _tx) {
   True
 }
 /// When a waiter (identified by their Credential) wants to take their share of the tips,
 /// this function ensures they leave half the ada in the stake pool for the restaurant.
 withdraw(_redeemer, waiter: Credential, tx: Transaction) {
   // Amount of ada the waiter is taking
   expect Some(waiter_tip_amount) = tx.withdrawals |> pairs.get_first(waiter)
   // Get all the UTxOs sent to the restaurant's address
   let restaurant_outputs =
     list.filter(tx.outputs, fn(o) { o.address == restaurant_addr })
   // Calculate the total ada sent to the restaurant
   let total_for_restaurant =
     list.foldl(restaurant_outputs, zero, fn(n, acc) { merge(n.value, acc) })
       |> lovelace_of()
   // Ensure the waiter leaves at least half the ada for the restaurant
   (2 * total_for_restaurant >= waiter_tip_amount)?
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:
stake_pool: The validator acts like a stake pool where customers can delegate ADA.
restaurant_addr: This represents the restaurant's address, where a portion of the ada should go.
publish: This is like a customer delegating their ada to a stake pool. Anyone can do it.
withdraw: This represents a waiter taking their share of the ada. The waiter is identified by their Credential. The validator ensures that whenever a waiter withdraws their ada, they leave at least half the amount in the jar for the restaurant.

1. Importing Modules:

```rust
use aiken/collection/pairs
use cardano/address.{Address, Credential}
use cardano/assets.{lovelace_of, merge, zero}
use cardano/transaction.{Transaction}
```

These lines import necessary modules.
aiken/collection/pairs: Provides functions for working with pairs (key-value pairs).
cardano/address: Provides types for working with Cardano addresses and credentials (used to identify users).
cardano/assets: Provides functions for working with Cardano assets, including ada 
cardano/transaction: Provides types for working with Cardano transactions.

2. Validator Definition:
/// A restaurant has a stake pool where customers can delegate their ada.
/// This validator manages the stake pool and ensures fair distribution.
validator stake_pool(restaurant_addr: Address) {

This defines a validator named stake_pool. 
restaurant_addr: Addres is a parameter to the validator, representing the address of the restaurant. This address will be used to ensure that a portion of the ada always goes to the restaurant.

3. publish handler:

```rust
 /// Allow anyone to add adato the tip jar. This is like a customer leaving a tip.
 publish(_redeemer, _certificate, _tx) {
   True
 }
```

The publish handler always returns True, meaning anyone can publish a certificate.
The _redeemer, _certificate, and _tx are parameters that are discarded (hence the underscore).

4. withdraw handler:
```rust
 /// When a waiter (identified by their Credential) wants to take their share of the ada,
 /// this function ensures they leave half the ada in the jar for the restaurant.
 withdraw(_redeemer, waiter: Credential, tx: Transaction) {
 …
 …
 else(_) {
   fail
 }
}
```

The withdraw handler uses waiter: Credential is the credential identifying the waiter.
tx: Transaction represents the transaction being evaluated
The redeemer, _redeemer, is discarded.

5. Calculating the Waiter's Tip:
  // Amount of ada the waiter is taking
   expect Some(waiter_tip_amount) = tx.withdrawals |> pairs.get_first(waiter)  
This line calculates the amount of ada the waiter is trying to withdraw.
tx.withdrawals is a list of pairs, where each pair contains a credential (identifying who is withdrawing) and the amount they are withdrawing.
pairs.get_first(waiter) finds the pair corresponding to the waiter credential.
expect Some(waiter_tip_amount) = … ensures that the waiter has a withdrawal in this transaction. If not, the transaction fails.
Pair is a specific type in Aiken for representing a pair of values that are not necessarily equal types. So a Pair<a, b> is similar, or the same, as a tuple (a, b). Like for tuples, you can access elements of a pair using the ordinal syntax:
let member = Pair(10, "Bloggs")
member.1st == 10
member.2nd == "Bloggs"
The reason there is this extra type Pair, where tuple might suffice, is to do with the underlying Plutus virtual machine, and explained in detail in the docs.

6. Finding Outputs Sent to the Restaurant:
```rust
 // Get all the UTxOs sent to the restaurant's address
   let restaurant_outputs =
     list.filter(tx.outputs, fn(o) { o.address == restaurant_addr })
```

This line finds all the outputs in the transaction that are being sent to the restaurant's address.
tx.outputs is a list of all outputs in the transaction.
 list.filter creates a new list containing only the outputs that satisfy the given condition (i.e., the output's address matches the restaurant_addr).

7. Calculating the Total ada for the Restaurant:
```rust
   let total_for_restaurant =
     list.foldl(restaurant_outputs, zero, fn(n, acc) { merge(n.value, acc) })
       |> lovelace_of()
```

This line calculates the total amount of ada being sent to the restaurant in this transaction.
 list.foldl iterates over the restaurant_outputs, starting with an initial value of zero (representing zero ada).
For each output n, it merges its value (n.value) with the accumulated value (acc) using the merge function.
lovelace_of() extracts the amount of ada from the merged value.

8. Ensuring Fair Distribution:
```rust
   (2 * total_for_restaurant >= waiter_tip_amount)?
 }
```
This line checks if the waiter is leaving at least half of the ada for the restaurant.
It multiplies total_for_restaurant by 2 and checks if it's greater than or equal to waiter_tip_amount.

9. Catch-All Condition:
```rust
 else(_) {
   fail
 }
}
```
This is a catch-all condition that causes the validator to fail if none of the previous validators return True
