# Aiken Validator : Order Up

To mitigate a common risk known as double-spending, or double satisfaction, it’s imperative that you make sure outputs associated with an input are NOT counted more than once. A common mistake is to only consider the input in a validator’s logic while neglecting to ensure the associated output is unique.

One way to achieve this is by tagging our outputs with a value unique to its corresponding input. We can use something from the OutputReference of the input and attach it as a unique tag to its associated outputs. This validator acts like a digital cash register:

- It verifies that a customer is paying for a valid order (with a Menu).
- It identifies the specific items on the bill (table_orders) belonging to the customer.
- It calculates the total amount paid.
- It ensures that the total paid is enough to cover the bill (menu.price).


```aiken
use aiken/collection/list
use aiken/crypto.{Blake2b_224, Hash, VerificationKey}
use cardano/address
use cardano/assets.{lovelace_of, merge}
use cardano/transaction.{InlineDatum, Output, OutputReference, Transaction}
type CustomerId =
 Hash<Blake2b_224, VerificationKey>
pub type Menu {
 customer: CustomerId,
 price: Int,
}
validator order_up {
 spend(
   // Use the 'spend' handler here
   optional_menu: Option<Menu>,
   _order: Data,
   table_number: OutputReference,
   self: Transaction,
 ) {
   expect Some(menu) = optional_menu
   let customer = address.from_verification_key(menu.customer)
   // Gather all the orders from the table with the same menu
   let table_orders =
     list.filter(
       self.outputs,
       fn(output) {
         when output.datum is {
           InlineDatum(output_datum) ->
            // Check if the order is for the correct customer and table
             if output_datum is OutputReference {
               and {
                 output.address == customer,
                 table_number == output_datum,
               }
             } else {
               False
             }
           _ -> False
         }
       },
     )
   // Calculate the total bill for the table
   let total_paid =
     list.foldl(
       table_orders,
       assets.zero,
       fn(order, total) { merge(order.value, total) },
     )
   // Ensure the total paid is greater than or equal to the price on the menu
   (lovelace_of(total_paid) >= menu.price)?
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:
This Aiken code defines a validator script called order_up. 

**1. Importing Modules:**
- use aiken/collection/list: Imports functions for working with lists (like filtering and summing).
- use aiken/crypto.{Blake2b_224, Hash, VerificationKey}: Imports cryptographic tools for creating unique identifiers from customer information.
- use cardano/address: Imports functions for working with Cardano addresses.
- use cardano/assets.{lovelace_of, merge}: Imports functions for handling ada and combining different asset values.
- use cardano/transaction.{InlineDatum, Output, OutputReference, Transaction}: Imports types and functions related to Cardano transactions.

**2. Defining Types:**
- type CustomerId = Hash<Blake2b_224, VerificationKey>: Defines a CustomerId type, which is a unique identifier created by hashing a customer's verification key (like a digital fingerprint).
- pub type Menu { customer: CustomerId, price: Int }: Defines a Menu type representing a restaurant menu. It includes the CustomerId of the customer who ordered and the price of the meal in Lovelace.

**3. Defining the order_up Validator:**
- validator order_up { … }: This defines a validator named order_up. 

**4. The spend Handler:**
- spend(optional_menu: Option<Menu>, _order: Data, table_number: OutputReference,  self: Transaction,) { … }: This is the spend handler, triggered when a customer tries to pay for their meal (spend funds from an output locked by this validator).
    - optional_menu: Option<Menu>: This represents the menu associated with the order. 
    - _order: Data: This represents additional order details, but it's not used in this code (hence the underscore).
    - table_number: OutputReference: This is a unique identifier for the 'table' (the UTxO being spent).
    - self: Transaction: This represents the entire transaction, giving access to all its details.

**5. Inside the spend Handler:**
- expect Some(menu) = optional_menu: This line ensures that a Menu is provided; otherwise, the script fails, similar to refusing payment if there's no order in the system.
- let customer = address.from_verification_key(menu.customer): This extracts the customer's Cardano address from their CustomerId.
- let table_orders = list.filter( …): This filters the transaction's outputs (self.outputs) to find only the outputs that belong to the current customer and match the table_number. It's like checking which items on the bill belong to the current table.
- let total_paid =  list.foldl( … ): This calculates the total amount of ada paid by the customer by summing up the values of the table_orders. It's like adding up all the items on the bill.
- (lovelace_of(total_paid) >= menu.price)?: This is the crucial check. It ensures that the total_paid by the customer in ada (lovelace_of) is greater than or equal to the price specified in the Menu. If not, the script fails, like rejecting the payment if it's less than the bill.

**6. The else Clause:**
- else(_) { fail }: This clause makes sure that the validator only allows spending transactions. Any other kind of transaction will cause the script to fail.

## More advanced examples
Hungry for more patterns? Luckily there is a growing brains trust willing to share design patterns and establish best practice. The following is not a comprehensive list, but a good starting point:
- Common Design Patterns - Anastasia Labs offer free audits for projects willing to open source their code. They also provide a collection of tried and tested modules and functions for implementing common design patterns.
- Cardano Capture The Flag - Vacuum Labs created a  game where developers and enthusiasts can try to exploit purposely vulnerable smart contracts, and in doing so, learn about the most common security issues and how to prevent them.
