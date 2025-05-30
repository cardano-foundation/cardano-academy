# You can handle this

Validator handlers
You can promote functions to validator handlers with the validator keyword. A validator is a named block that contains one or more of the following 6 handlers: mint, spend, withdraw, publish, vote or propose.

Like expressions and blocks, handlers are also evaluated as predicates which return True or False. Each handler is a function taking three arguments:
A redeemer, which is a user-defined type and value usually provided when the UTxO is being consumed.
A target, whose type matches the corresponding purpose.
A transaction representing the script execution context.
The spend handler also takes an optional first argument, a user-defined datum. The Aiken documentation summarises this neatly with the following table. 

**Figure 53**: Aiken Purposes
Our first Aiken validator script ensures that a restaurant reservation is valid only if:
The person using the reservation is the same person it was reserved for.
The reservation is used before its expiry time.

```rust
use cardano/transaction.{OutputReference, Transaction}
use helpers/arrive.{must_be_dined_by, must_dine_before_expiry}
use types/arrive_on_time.{ReservationDetails}

//Restaurant reservation validator
validator validate_reservation {
 spend(
   datum: Option<ReservationDetails>,
   _redeemer: Void,
   _output_reference: OutputReference,
   tx: Transaction,
 ) {

   expect Some(details) = datum
   and {
     // the customer dining must match the reservation
     must_be_dined_by(tx.extra_signatories, details.reserved_for)?,
     // the dining time must be before the reservation expires
     must_dine_before_expiry(tx.validity_range, details.reservation_expiry)?,
   }
 }

 // for other script purposes, the transaction is invalid
 else(_) {
   fail
 }
}
```

## Explaining the code:

This code defines a validator for a restaurant reservation. 

Lines 1-3: Importing Modules
use cardano/transaction.{OutputReference, Transaction}: This imports types related to transactions, including OutputReference (a reference to a previous transaction output) and Transaction (representing the Cardano transaction being validated).
use helpers/arrive.{must_be_dined_by, must_dine_before_expiry}: This imports helper functions from the custom module helpers/arrive we coded earlier.
use types/arrive_on_time.{ReservationDetails}: This imports a custom data type called ReservationDetails from the types/arrive_on_time module.
Lines 5-22: Validator Definition
validator validate_reservation { ... }: This defines a validator named validate_reservation.
Lines 6-18: spend Handler
spend( ... ) { ... }: This is the spend handler within the validator. It defines the logic that must be satisfied when funds are being spent from an output locked by this validator script.
datum: Option<ReservationDetails>: This expects an optional datum (data attached to an output) of type ReservationDetails. This datum  holds the reservation information.
_redeemer: Void: This indicates that the redeemer (data provided by the user when spending the output) is not used in this validator. The underscore _ signifies that the redeemer is unused.
_output_reference: OutputReference: This represents the output reference being spent, but it's not used in this validator.
tx: Transaction: This provides access to the current transaction being validated.
Lines 11-17: Validation Logic
expect Some(details) = datum: This line checks if the datum is present. If it is, it extracts the ReservationDetails and assigns them to the variable details. If the datum is not present, the script execution halts.
and { ... }: This ensures that both of the following conditions are met:
must_be_dined_by(tx.extra_signatories, details.reserved_for)?: This line calls the must_be_dined_by helper function to check if the person spending the funds (represented by tx.extra_signatories) matches the person for whom the reservation was made (details.reserved_for). 
must_dine_before_expiry(tx.validity_range, details.reservation_expiry)?: This line calls the must_dine_before_expiry function to check if the transaction is being submitted before the reservation expiry time. tx.validity_range provides the time range during which the transaction is valid. 

This is our first encounter with the expect keyword.  expect is an assignment keyword a bit like let, except it allows potentially unsafe conversions. It’s used for two scenarios: 
To let the compiler know to do a non-exhaustive pattern-match. For example, when you’re interested in only one outcome, otherwise it will crash your validator. This may seem to be a bit drastic, but running validators on Cardano doesn’t facilitate error-handling, so either the data has the expected shape, or the validator fails.
Casting from Data to a custom type. You can use expect to convert an opaque Data into a more concrete type. With Aiken validators, we usually find Data in the datums attached to outputs. 
There is some more nuance as to when you should use expect with when/is and if/is. Read more about this in the documentation. If you haven’t already, you should join Aiken’s discord server where common questions are answered such as Difference between let and expect explained as follows:
let enables you to do what is called "destructuring". This means pull apart the different constituents of a given element. If that element does not have exactly the structure you are describing, the compiler will let you know there is an error, because it cannot guarantee that your destructuring is correct. In contrast, expect enables you to "attempt" destructuring something into the shape you are describing. This is useful when the compiler cannot know at compile time what shape your structure may have. For example when it is an enum, and can have any shape of the different variant types. Instead of the compiler checking at compile time, the code will check at run time that it has the correct shape, and crash otherwise.

So when there is a single possible shape, use let. When the shape is unknown at compile time, use expect.

## And && or

As everything is an expression, or predicate returning a Bool, you'll soon encounter long chains of logical operators when coding more complex validators, eg. 
True && False && True || False
As these boolean checks are so ubiquitous in Aiken validators, you can use more user-friendly keywords in place of logical operators.
and {
 True,
 False,
 or {
   True,
   False,
 }
}
Lines 20-22: Fallback Handler
else(_) { fail: This is a catch-all condition. If the script reaches this point (i.e., it's not a spend transaction), it automatically fails. This ensures that the validator only allows spending transactions that meet the defined reservation conditions. Think of it as being like a safety feature that knocks off the oven if certain criteria are not met. 
