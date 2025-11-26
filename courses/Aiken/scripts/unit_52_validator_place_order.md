# Aiken Validator : Place Order

This validator script ensures that when a customer places an order:
- The transaction includes an output sent to the correct restaurant's address.
- The amount of ada in that output is greater than or equal to the bill amount for the order.

```aiken
use aiken/collection/list
use cardano/assets.{lovelace_of}
use cardano/transaction.{OutputReference, Transaction}
use types/place_order.{Datum}
validator place_order {
 spend(datum: Option<Datum>, _redeemer: Void, _output_reference: OutputReference, tx: Transaction) {
   expect Some(d) = datum
   // Customer is spending money to pay the bill
   expect Some(_restaurant_output) =
     list.find(
       // Find the payment going to the restaurant
       tx.outputs,
       fn(output) { and {
           // Check both conditions:
           output.address == d.restaurant,
           // Payment is sent to the correct restaurant
           lovelace_of(output.value) >= d.billAmount,
         } },
     )
   // Payment covers the bill
   True
   // If both conditions are met, the order is valid
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:

Lines 1-4: Importing Modules with ‘use’ keyword:
- use aiken/collection/list: This line imports functions for working with lists, which will be used to search through transaction outputs.
- use cardano/assets.{lovelace_of}: This line imports the lovelace_of function, used to extract the amount of ada (Lovelace) from a value.
- use types/place_order.{Datum}: This line imports a custom data type called Datum from the module types/place_order. This type holds information relevant to the order, such as the restaurant's address and the bill amount.

Lines 5-25: Validator Definition
- validator place_order { ... }: This defines a validator named place_order.

Lines 6-23: spend Handler
- spend(datum: Option<Datum>, _redeemer: Void, _output_reference: OutputReference, tx: Transaction) { ... }: This is the spend handler within the validator. It defines the logic that must be satisfied when funds are spent from an output locked by this validator script.
    - datum: Option<Datum>: This expects an optional datum of type Datum. This datum holds the order information.
    - _redeemer: Void This indicates that the redeemer (data provided by the user when spending the output) is not used in this validator.
    - _output_reference: OutputReference: This represents the output reference being spent, but it's not used in this validator.
    - tx: Transaction: This provides access to the current transaction being validated.

Lines 7-19: Validation Logic
- expect Some(d) = datum: This line checks if the datum is present. If it is, it extracts the Datum and assigns it to the variable d. If the datum is not present, the script execution halts.

- expect Some(_restaurant_output) =  list.find(...): This line attempts to find an output within the transaction that meets specific conditions:
    - tx.outputs: This provides the list of outputs in the transaction.
    - fn(output) { and { : This is an anonymous function we coded earlier that defines the search criteria for each output.
        - output.address == d.restaurant: This checks if the output's address matches the restaurant's address from the datum.
        - lovelace_of(output.value) >= d.billAmount,: This checks if the amount of ada in the output is greater than or equal to the billAmount from the datum.
True: If an output meeting both conditions is found, this line ensures the script succeeds.

Lines 21-23: Fallback Handler
-  else(_) { fail }: This is a catch-all condition, for any scenario not catered for above.
