# 58. Did that go through? 

This code defines a validator that ensures a customer pays their bill correctly in our restaurant. This is slightly different than earlier, but with the same goal. Specifically, the validator script ensures that a bill payment is valid only if:
The transaction includes an output sent to the correct restaurant's address.
The amount of ada in that output is greater than or equal to the total cost of the bill.

```aiken
use aiken/collection/list
use cardano/assets.{lovelace_of}
use cardano/transaction.{OutputReference, Transaction}
use types/pay_bill.{Datum}
validator bill_paid {
 // Ensure the purpose of this transaction is spending funds (to pay the bill)
 spend(
   datum: Option<Datum>,
   _redeemer: Void,
   _output_reference: OutputReference,
   tx: Transaction,
 ) {
   expect Some(d) = datum
   // Find the output (payment) that goes to the correct restaurant
   expect Some(_restaurant_output) =
     list.find(
       tx.outputs,
       fn(output) {
         // Check if:
         // - The output's address is the restaurant's address
         // - The lovelace value of the output is equal to or more than the total cost
         output.address == d.restaurant && lovelace_of(output.value) >= d.total_cost
       },
     )
   True
   // If both conditions are met, the transaction is valid
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:

Lines 1-4: Importing Modules
use types/pay_bill.{Datum}: This imports a custom data type called Datum from the types/pay_bill module. This type holds information related to the bill, such as the restaurant's address and the total cost.

Lines 5-26: Validator Definition
validator bill_paid { … }: This defines a validator named bill_paid. 

Lines 6-24: spendHandler
spend( ... ) { ... }: This is the spend handler within the validator. It defines the logic that must be satisfied when funds are being spent from an output locked by this validator script.
datum: Option<Datum>: This expects an optional datum of type Datum. This datum holds the bill information.
_redeemer: Void: This indicates that the redeemer (data provided by the user when spending the output) is not used in this validator.
_output_reference: OutputReference: This represents the output reference being spent, but it's not used in this validator.
tx: Transaction: This provides access to the current transaction being validated.

Lines 11-21: Validation Logic      
expect Some(d) = datum: This line checks if the datum is present. If it is, it extracts the Datum and assigns it to the variable d. If the datum is not present, the script execution halts.
expect Some(_restaurant_output) = list.find( … ): This line attempts to find an output within the transaction that meets the following conditions:
tx.outputs: This provides the list of outputs in the transaction.
fn(output) { … }: This is an anonymous function that defines the search criteria for each output.
output.address == d.restaurant: This checks if the output's address matches the restaurant's address from the datum.
lovelace_of(output.value) >= d.total_cost: This checks if the amount of ada in the output is greater than or equal to the total cost from the datum.
True: If an output meeting both conditions is found, this line ensures the script succeeds.

Lines 23-25: Fallback Handler
else(_) { fail }: This is a catch-all condition, and behaves the same way to the onewe described earlier. 
