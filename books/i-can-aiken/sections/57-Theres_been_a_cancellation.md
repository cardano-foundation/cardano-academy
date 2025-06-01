# 57. There’s been a cancellation

This validator script ensures that a restaurant reservation cancellation is valid only if:
The cancellation occurs before the reservation expires.
A valid cancellation code (less than or equal to 0) is provided.

```rust
use aiken/interval.{Finite}
use cardano/transaction.{OutputReference, Transaction}
use types/cancellation.{Reservation}
validator validate_cancellation {
 spend(
   datum: Option<Reservation>,
   cancellation_code: Int,
   _output_reference: OutputReference,
   tx: Transaction,
 ) {
   expect Some(d) = datum
   // When the customer is attempting to cancel the reservation
   let Reservation { expiration_time } = d
   let is_expired = tx.validity_range.lower_bound.bound_type
   when is_expired is {
     Finite(cancellation_time) ->
       expiration_time <= cancellation_time && cancellation_code <= 0
     _ -> False
   }
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:

Lines 1-3: Importing Modules
use aiken/interval.{Finite}: This imports the Finite type from the aiken/interval module. This type is used to represent a specific point in time within an interval.
use types/cancellation.{Reservation}: This imports a custom data type called Reservation from the types/cancellation module we created earlier. This type holds information about the reservation, including its expiration time.

Lines 5-22: Validator Definition
validator validate_cancellation { … }: This defines a validator named validate_cancellation. 

Lines 6-20: spend Handler
spend( ... ) { ... }: This is the spend handler within the validator. It defines the logic that must be satisfied when funds are being spent from an output locked by this validator script.
datum: Option<Reservation>: This expects an optional datum (data attached to an output) of type Reservation. This datum holds the reservation information.
cancellation_code: Int: This expects an integer value representing a cancellation code provided as the redeemer.
_output_reference: OutputReference: This represents the output reference being spent, but it's not used in this validator.
tx: Transaction: This provides access to the current transaction being validated.

Lines 11-18: Validation Logic
expect Some(d) = datum: This line checks if the datum is present. If it is, it extracts the Reservation data and assigns it to the variable d. If the datum is not present, the script execution halts.
let Reservation { expiration_time } = d: This line extracts the expiration_time field from the Reservation data and assigns it to a variable.
let is_expired = tx.validity_range.lower_bound.bound_type: This line retrieves the lower bound of the transaction's validity range and extracts its type. This is used to determine the time of the cancellation attempt.
when is_expired is { ... }: This when expression checks the type of is_expired and performs different actions based on the type:
Finite(cancellation_time) -> ...: If is_expired is a Finite value (meaning the transaction has a specific start time), it extracts the time into cancellation_time and proceeds with the following check:
expiration_time <= cancellation_time && cancellation_code <= 0: This checks if the reservation's expiration_time is less than or equal to the cancellation_time (ensuring the cancellation happens before the reservation expires) and if the cancellation_code is less than or equal to 0 ( representing a valid cancellation code). Both conditions must be True for the script to succeed.
 _ -> False: If is_expired is any other type, this condition evaluates to False, causing the script to fail.

Lines 20-22: Fallback Handler
else(_) { fail }: This is a catch-all condition. If the script reaches this point (i.e., it's not a spend transaction), it automatically fails. This ensures that the validator only allows spending transactions that meet the defined cancellation conditions.
