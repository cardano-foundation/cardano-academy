# Aiken Validator : Loyalty Points & Rewards

This code defines a validator script named redeem_reward that manages a reward system based on points earned by members. Specifically, this validator script manages a reward system by checking these conditions when a member tries to redeem a reward:
- Member Identification: The member trying to redeem the reward is identified through their ID hash.
- Points Earned: The member has earned enough loyalty points to be eligible for redeeming a reward.
- Sufficient Points: The member has enough points to redeem the specific reward, considering the transaction's validity range.

```aiken
use cardano/transaction.{OutputReference, Transaction}
use helpers/vest.{points_earned, points_sufficient}
use types/vesting.{Datum}
validator redeem_reward {
 spend(
   datum: Option<Datum>,
   _redeemer: Void,
   _output_reference: OutputReference,
   tx: Transaction,
 ) {
   expect Some(d) = datum
   // Get the transaction details
   let Transaction { extra_signatories, validity_range, .. } = tx
   and {
     // If the member wants to redeem... Check membership card
     // …then check points earned
     points_earned(extra_signatories, d.member_id_hash)?,         
     points_sufficient(validity_range, d.required_points)?,
   }   
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:

Lines 1-4: Importing Modules
- use helpers/vest.{points_earned, points_sufficient}: This line imports helper functions from the helpers/vest module,  containing logic for:
    - points_earned: Checking if a member has earned enough points.
    - points_sufficient: Checking if the member has sufficient points to redeem a reward.
- use types/vesting.{Datum}: This line imports a custom data type called Datum from the module types/vesting. This type holds information relevant to the reward system, such as the member's ID and the required points for redeeming a reward.

Lines 5-6: Validator Definition
- validator redeem_reward { … }: This defines a validator named redeem_reward. 

Lines 6-21: spend handler
- spend(datum: Option<Datum>, _redeemer: Void, _output_reference: OutputReference, tx: Transaction) { ... }: This is the spend handler within the validator. It defines the logic that must be satisfied when funds are spent from an output locked by this validator script.
    - datum: Option<Datum>: This expects an optional datum of type Datum. This datum holds the reward system information.
    - _redeemer: Void: This indicates that the redeemer (data provided by the user when spending the output) is not used in this validator.
    - _output_reference: OutputReference: This represents the output reference being spent, but it's not used in this validator.
    - tx: Transaction: This provides access to the current transaction being validated.

Lines 11-18: Validation Logic
- expect Some(d) = datum: This line checks if the datum is present. If it is, it extracts the Datum data and assigns it to the variable d. If the datum is not present, the script execution halts.
- let Transaction { extra_signatories, validity_range, .. } = tx: This line extracts the extra_signatories and validity_range (the time range during which the transaction is valid) from the transaction.
- and { … }: This and block combines multiple conditions that must all be True for the script to succeed.
    - points_earned(extra_signatories, d.member_id_hash)?: This line calls the helper function points_earned to check if the member (identified by d.member_id_hash) has earned enough points.
    - points_sufficient(validity_range, d.required_points)?: This line calls the helper function points_sufficient to check if the member has sufficient points to redeem a reward, possibly considering the validity_range of the transaction.

Lines 20-22: Fallback Handler
- else(_) { fail }: This is a catch-all condition, and behaves the same way to the one we described earlier. 
