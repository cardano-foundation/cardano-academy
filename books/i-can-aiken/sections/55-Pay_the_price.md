# 55. Pay the price

This code defines a validator that ensures a customer pays the correct amount for their order. Specifically, this validator script ensures that when a customer pays for their order:
The transaction includes outputs sent to the restaurant's address.
The total amount of ada paid to the restaurant is greater than or equal to the total cost of the order.

```rust
use aiken/collection/list
use cardano/assets
use cardano/transaction.{OutputReference, Transaction}
use types/confirm_payment.{OrderDetails, RestaurantPolicy}
validator validate_payment(policy: RestaurantPolicy) {
 // when customer is paying for their order
 spend(
   datum: Option<OrderDetails>,
   _redeemer: Data,
   _output_reference: OutputReference,
   tx: Transaction,
 ) {
   expect Some(order) = datum
   // get the transaction outputs
   let Transaction { outputs, .. } = tx
   // Get only the outputs that go to the restaurant's address
   let restaurant_outputs =
    list.filter(outputs, fn(o) { o.address == policy.restaurant_address })
   // Calculate the total amount paid to the restaurant
   let total_paid =
     list.foldl(
       restaurant_outputs,
       assets.zero,
       fn(n, acc) { assets.merge(n.value, acc) },
     )
   // Check if the customer paid enough
   (assets.lovelace_of(total_paid) >= order.total_cost)?
 }
 // Reject any other script purpose
 else(_) {
   fail
 }
}
```

## Explaining the code:

Lines 1-4: Importing Modules
use cardano/assets: This imports functions for handling Cardano assets and values from the cardano/assets module.
use types/confirm_payment.{OrderDetails, RestaurantPolicy}: This imports custom types OrderDetails and RestaurantPolicy from the types/confirm_payment custom module coded earlier. These types hold information about the order and the restaurant's payment policy.

Lines 5-29: Validator Definition
validator validate_payment(policy: RestaurantPolicy) { .. }: This defines a validator named validate_payment that takes a RestaurantPolicy value as a parameter.

Lines 6-27: spend Handler
spend( ... ) { ... }: This is the spend handler within the validator, defining the logic for validating a payment transaction.
datum: Option<OrderDetails>: This expects an optional datum of type OrderDetails, which contains information about the customer's order.
_redeemer: Data: This indicates that the redeemer (data provided by the user when spending the output) is not used in this validator.
_output_reference: OutputReference: This represents the output reference being spent, but it's not used in this validator.
tx: Transaction: This provides access to the current transaction being validated.

Lines 11-25: Validation Logic
expect Some(order) = datum: This line checks if the datum is present and extracts the OrderDetails into the order variable. If the datum is missing, the script execution halts.
let Transaction { outputs, .. } = tx: This line extracts the outputs field from the Transaction object.
This is our first encounter with the 'spread operator'. Use this if you want to pull only specific named fields out, or it can be nothing at all, whereby you can use it as a placeholder. The spread operator tells the compiler that everything else can be ignored.
 let restaurant_outputs =
    list.filter(outputs, fn(o) { o.address == policy.restaurant_address }): This line filters the transaction outputs, keeping only those sent to the restaurant's address (obtained from the policy parameter).
 let total_paid = list.foldl( … ): This line calculates the total amount paid to the restaurant by iterating over the restaurant_outputs:
restaurant_outputs: The list of outputs to iterate over.
assets.zero: The initial value for the accumulator ( representing an empty value).
 fn(n, acc) { assets.merge(n.value, acc) }: A function that merges the value of each output (n.value) with the accumulator (acc). Look it up in the standard library if not sure. 

If not sure about a function, look it up in the standard library. In this case, foldl which performs a left-to-right fold operation on a collection of key-value pairs. 
 (assets.lovelace_of(total_paid) >= order.total_cost)?: This line checks if the total amount of Lovelace in total_paid is greater than or equal to the total_cost from the order details. 

Lines 27-29: Fallback Handler
else(_) { fail }: This catch-all condition ensures that the script fails for any transaction that is not a spending transaction.
