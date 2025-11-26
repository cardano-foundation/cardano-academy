# Aiken Validator : Tipping Jar

This code defines a validator script named tips that manages a tipping system. This system allows users to add tips to a tip jar and allows the owner of the jar to claim the accumulated tips. Specifically, this validator script manages a tipping system by allowing two actions:
- Adding a Tip: Ensures that the tip amount meets the minimum requirement and that the datum is correctly updated.
- Claiming Tips: Allows only the owner of the tip jar to claim the accumulated tips.

```aiken
use aiken/collection/list
use cardano/address.{Script}
use cardano/assets.{lovelace_of}
use cardano/transaction.{
 InlineDatum, OutputReference, Transaction, find_input, find_script_outputs,
}
use helpers/tip.{count_input_scripts, datum_is_correct, minimum_tip}
use types/tipping.{AddTip, Claim, Datum, Redeemer}
// Main Validator Script
validator tips {
 spend(
   datum: Option<Datum>,
   redeemer: Redeemer,
   output_reference: OutputReference,
   tx: Transaction,
 ) {
   expect Some(d) = datum
   let tx_inputs = tx.inputs
   let tx_outputs = tx.outputs
   expect Some(own_input) = find_input(tx_inputs, output_reference)
   expect Script(own_hash) = own_input.output.address.payment_credential
   let script_outputs = find_script_outputs(tx_outputs, own_hash)


   // Ensure only one script input
   expect count_input_scripts(tx_inputs) == 1
   // Ensure only one script output
   expect list.length(script_outputs) == 1
   expect Some(script_output) = list.head(script_outputs)
   expect InlineDatum(output_datum_raw) = script_output.datum
   expect output_datum: Datum = output_datum_raw
   when redeemer is {
     AddTip -> and {
         // Corrected Minimum tip requirement (bool)
         (lovelace_of(own_input.output.value) + minimum_tip <= lovelace_of(
           script_output.value,
         ))?,
         // Data integrity check
         datum_is_correct(d, output_datum)?,
       }
     // Owner claiming the tips
     Claim -> list.has(tx.extra_signatories, d.owner)
   }
 }
 else(_) {
   fail
 }
}
```

## Explaining the code:

Lines 1-7: Import Modules
- use aiken/collection/list: This imports functions for working with lists, like length, head, and has.
- use cardano/address.{Script}: This imports the Script type for working with script addresses.
- use cardano/transaction.{ InlineDatum, OutputReference, Transaction, find_input, find_script_outputs }: This imports types and functions for working with Cardano transactions, including finding specific inputs and outputs.
- use helpers/tip.{count_input_scripts, datum_is_correct, minimum_tip}: This imports helper functions from the helpers/tip module, containing logic for:
    - count_input_scripts: Counting the number of script inputs in a transaction.
    - datum_is_correct: Checking if the datum is correctly updated.
    - minimum_tip: Determining the minimum tip amount.
- use types/tipping.{AddTip, Claim, Datum, Redeemer}: This imports custom data types from the types/tipping module,  including:
    - AddTip: A constructor for the Redeemer type, representing adding a tip.
    - Claim: A constructor for the Redeemer type, representing claiming the tips.
    - Datum: A data type holding information about the tip jar, such as the owner's address.
    -  Redeemer: An enumeration representing the actions that can be performed (add a tip or claim the tips).

Lines 9-42: Validator Definition
- validator tips { … }: This defines the validator named tips.

Lines 10-40: spend Handler
- spend( datum: Option<Datum>, redeemer: Redeemer, output_reference: OutputReference,  tx: Transaction ) { … }: This is the spend handler within the validator. It defines the logic that must be satisfied when funds are spent from an output locked by this validator script.
    - datum: Option<Datum>: This expects an optional datum of type Datum. 
    - redeemer: Redeemer: This expects a Redeemer value representing the action to be performed (add a tip or claim the tips).
    - output_reference: OutputReference: This represents the output reference being spent.
    - tx: Transaction: This provides access to the current transaction being validated.

Lines 15-23: Transaction and Script Output Handling  
- expect Some(d) = datum: This line checks if the datum is present and extracts the Datum data.
- let tx_inputs = tx.inputs: This line gets all inputs of the transaction.
- let tx_outputs = tx.outputs: This line gets all outputs of the transaction.
- expect Some(own_input) = find_input(tx_inputs, output_reference): This line finds the input being spent in the transaction.
- expect Script(own_hash) = own_input.output.address.payment_credential: This line ensures the input is a script input and gets the script hash.
- let script_outputs = find_script_outputs(tx_outputs, own_hash): This line finds all outputs in the transaction that are locked by the same script.

Lines 25-28: Input and Output Checks 
- expect count_input_scripts(tx_inputs) == 1: This line ensures that there is only one script input in the transaction.
- expect list.length(script_outputs) == 1: This line ensures that there is only one script output in the transaction.
- expect Some(script_output) = list.head(script_outputs): This line gets the single script output from the list.
- expect InlineDatum(output_datum_raw) = script_output.datum: This line ensures the script output has an inline datum.
- expect output_datum: Datum = output_datum_raw: This line extracts the Datum from the output's inline datum.

Lines 30-38: Redeemer Handling
- when redeemer is { … }: This when expression checks the value of the redeemer and performs different validations based on the action:
    - AddTip -> and { … }: If the action is AddTip: (lovelace_of(own_input.output.value) + minimum_tip <= lovelace_of(script_output.value))?: This line checks if the Lovelace amount in the output is greater than or equal to the Lovelace amount in the input plus the minimum tip amount.
datum_is_correct(d, output_datum)?: This line calls the helper function to check if the datum is correctly updated.
    - Claim -> list.has(tx.extra_signatories, d.owner): If the action is Claim, this line checks if the transaction is signed by the owner of the tip jar.

Lines 40-42: Fallback Handler
-  else(_) { fail }: This is a catch-all condition. If the script reaches this point (i.e., it's not a spend transaction), it automatically fails. 
