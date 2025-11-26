# Aiken Validator : VIPs Only

This validator script controls access to VIP members’ bar by checking two conditions:
- Secret Code Word: The user must provide the correct secret code word ('VIP007' in this case).
- VIP Identification: The transaction must be signed by the VIP member.

```aiken
use aiken/collection/list
use aiken/primitive/string
use cardano/transaction.{OutputReference, Transaction}
use types/vip.{Datum, Redeemer}
validator check_vip {
 spend(
   datum: Option<Datum>,
   redeemer: Redeemer,
   _output_reference: OutputReference,
   tx: Transaction,
 ) {
   Trace @”redeemer”: string.from_bytearray(redeemer.secret_code_word)
   expect Some(d) = datum
   let correct_code_word = redeemer.secret_code_word == "VIP007"
   let confirm_vip = list.has(tx.extra_signatories, d.vip_id)
   correct_code_word? && confirm_vip?
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:

Lines 1-4: Importing Modules
- use aiken/collection/list: This line imports functions for working with lists, specifically the has function to check if a list contains a specific element.
- use aiken/primitive/string: This line imports functions for working with strings, specifically the from_bytearray function to convert a byte array to a string.
- use types/vip.{Datum, Redeemer}: This line imports custom data types from the module types/vip. These include:
    - Datum: A data type holding information relevant to the VIP status, such as the VIP ID.
    - Redeemer: A data type holding information provided by the user when interacting with the script, such as the secret code word.

Lines 5-19: Validator Definition
- validator check_vip { … }: This defines a validator named check_vip.

Lines 6-17: spend Handler
- spend( datum: Option<Datum>, redeemer: Redeemer, _output_reference: OutputReference, tx: Transaction, ) { … }: This is the spend handler within the validator. It defines the logic that must be satisfied when funds are spent from an output locked by this validator script.
    - datum: Option<Datum>: This expects an optional datum of type Datum. This datum holds the VIP information.
    - redeemer: Redeemer: This expects a Redeemer value, which should contain the secret code word.
    - _output_reference: OutputReference: This represents the output reference being spent, but it's not used in this validator.
    - tx: Transaction: This provides access to the current transaction being validated.

Lines 11-15: Validation Logic
- Trace @”redeemer”: string.from_bytearray(redeemer.secret_code_word): The trace keyword here ensures that log messages are captured by the virtual machine for this expression. 
- expect Some(d) = datum: This line checks if the datum is present. If it is, it extracts the Datum data and assigns it to the variable d. If the datum is not present, the script execution halts.
- let correct_code_word = redeemer.secret_code_word == "VIP007": This line checks if the secret_code_word provided in the redeemer matches the expected code word 'VIP007'.
- let confirm_vip = list.has(tx.extra_signatories, d.vip_id): This line checks if the transaction is signed by the VIP member, identified by d.vip_id.
- correct_code_word? && confirm_vip?: This line combines the two checks using the && operator. This ensures that both conditions must be True for the script to succeed. If either correct_code_word? or confirm_vip is false, the script will fail.

Lines 17-19: Fallback Handler
-  else(_) { fail }: This is a catch-all condition. If the script reaches this point (i.e., it's not a spend transaction), it automatically fails. This ensures that the validator only allows spending transactions that meet the defined VIP access conditions.
