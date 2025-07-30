# 56. Service please!

This validator script manages orders in a restaurant setting with these key features:
Multiple Chef Signatures: Requires signatures from all chefs involved in an order.
Customer Verification: Verifies the customer's identity using their stake credential.
Two Handlers: Provides separate logic for marking an order as served (withdraw) and for spending the fulfilled order (spend).
This example shows how Aiken can be used to create a complex, multivalidator for managing workflows.

```aiken
use aiken/collection/list
use cardano/address.{Address, Inline, Script, StakeCredential}
use cardano/transaction.{ InlineDatum, Input, Output, OutputReference, Transaction,}
use types/service_please.{OrderDatum}
validator service_please {
 //Function to allow customer's dish to be served
 withdraw(_redeemer: Data, order_credential: StakeCredential, tx: Transaction) {
   let Transaction { reference_inputs, extra_signatories, .. } = tx
   //check that the order credential is inline and matches the customer's credential
   expect Inline(customer_cred) = order_credential
   expect Script(customer_hash) = customer_cred
   // Find the original order input.
   expect Some(order_input) =
     reference_inputs
       |> list.find(
           fn(input) {
             let Input {
               output: Output {
                 address: Address { payment_credential: payment_cred, .. },
                 ..
               },
               ..
             } = input
             //Make sure the payment credential matches the customer's hash
             when payment_cred is {
               Script(hash) -> hash == customer_hash
               _ -> False
             }
           },
         )
   //Ensure the order input has the order data.
   expect Input { output: Output { datum: InlineDatum(raw_datum), .. }, .. } = order_input
   expect order_datum: OrderDatum = raw_datum
   //Check if all the required chef signatures are present.
   list.all(order_datum.chef_hashes, fn(h) { list.has(extra_signatories, h) })
 }
 //Function to allow to spend/execute the order
 spend(
   datum: Option<OrderDatum>,
   _redeemer: Data,
   _output_reference: OutputReference,
   tx: Transaction,
 ) {
   //Expect the context to have a transaction.
   let Transaction { extra_signatories, .. } = tx
   //Get the list of required chef hashes from the reservation data.
   expect Some(order_datum) = datum
   //check if all the required chef signatures are present.
   list.all(orderDatum.chef_hashes, fn(h) { list.has(extra_signatories, h) })
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:

Lines 1-6: Importing Modules with ‘use’ keyword:
use aiken/collection/list: This imports functions for working with lists, like all, has, and find.
use cardano/address.{Address, Inline, Script, StakeCredential}: This imports types for working with Cardano addresses and stake credentials.
use cardano/transaction.{ InlineDatum, Input, Output, OutputReference, Transaction,}: This imports types for working with Cardano transactions.
use types/service_please.{OrderDatum}: This imports a custom data type OrderDatum, containing details about the order, including the chefs involved.

Lines 7-58: Validator Definition
validator service_please { ... }: This defines the validator named service_please.

Lines 8-39: withdraw Handler
withdraw(_redeemer: Data, order_credential: StakeCredential, tx: Transaction) { ... }: This defines the withdraw handler which handles the logic for marking an order as served.
_redeemer: Data: The redeemer (unused in this handler).
order_credential: StakeCredential: The stake credential associated with the order.
tx: Transaction: The current transaction.
let Transaction { reference_inputs, extra_signatories, .. } = tx: This extracts reference_inputs and extra_signatories from the transaction.
expect Inline(customer_cred) = order_credential: Ensures the order credential is an inline datum.
expect Script(customer_hash) = customer_cred: Further ensures the credential is a script credential and extracts the hash.
expect Some(order_input) = : This code block searches for the original order input within the reference_inputs:
reference_inputs |> list.find(...): Uses list.find to locate the input matching the criteria defined in the anonymous function we coded earlier.
Inside the anonymous function:
let Input { output: Output { address: Address {
 { payment_credential: payment_cred, .. }, …}, …} = input: Destructures the input to access the payment credential of the output's address. 
While we encountered constructors earlier, we can also leverage destructuring which is the opposite of constructing a value and uses a similar syntax but backwards to before. So what we saw earlier was constructors and fields appearing on the right-hand side of an assignment, but with destructuring, they are on the left-hand side. Using a restaurant meal as an example:

```aiken
// Constructing
let meal = Meal { menuName: "Waldorf Salad", calories: 500, rating: 5 }
// Destructuring
let Meal { menuName, calories, rating } = meal
menuName == "Waldorf Salad" // True
calories == 500 // True
rating == 5 // True
// ..is the same as…
let menuName = meal.name
let calories = meal.calories
let rating = meal.age
```

Destructuring is convenient here because the associated type has a single constructor and the identifiers introduced also have the same names as the fields. More advanced examples are in the aiken-lang.org docs.
when payment_cred is { … }: Checks if the payment credential is a script credential and if its hash matches the customer_hash.
 expect Input { output: Output { datum: InlineDatum(raw_datum), .. }, .. } =
order_input: Ensures the found input has an inline datum.
expect order_datum: OrderDatum = raw_datum: Extracts the OrderDatum from the raw datum.
list.all(orderDatum.chef_hashes, fn(h) { list.has(extra_signatories, h) }): Checks if all the chef hashes in orderDatum.chef_hashes are present in the transaction's extra_signatories.
Lines 41-56: spend Handler

```aiken
spend( datum: Option<OrderDatum>,
   _redeemer: Data,
   _output_reference: OutputReference,
   tx: Transaction,
 ) {
   //Expect the context to have a transaction.
   let Transaction { extra_signatories, .. } = tx
   //Get the list of required chef hashes from the reservation data.
   expect Some(order_datum) = datum
   //check if all the required chef signatures are present.
   list.all(orderDatum.chef_hashes, fn(h) { list.has(extra_signatories, h) })
 }
 else(_) {
   fail
```

spend( datum: Option<OrderDatum>,_redeemer: Data, _output_reference: OutputReference, tx: Transaction) { ... }: Defines the spend handler,  for spending the output that represents the fulfilled order.
datum: Option<OrderDatum>: The datum associated with the output.
_redeemer: Data: The redeemer (unused in this handler).
_output_reference: OutputReference: The output reference (unused in this handler).
tx: Transaction: The current transaction.
let Transaction { extra_signatories, .. } = tx: Extracts the extra_signatories from the transaction.
expect Some(order_datum) = datum: Ensures the datum is present and extracts the order_datum. Assigns the extracted datum to order_datum.
list.all(orderDatum.chef_hashes, fn(h) { list.has(extra_signatories, h) }): Checks if all the chef hashes in orderDatum.chef_hashes are present in the transaction's extra_signatories.
Lines 57-58: Fallback Handler
else(_) { fail }: This catch-all condition fails the script for any transaction that is not a spend or withdraw.
