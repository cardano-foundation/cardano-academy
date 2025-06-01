# 51. Multiple Validators

**/validators/banned-customers/bc.ak**

Next, we’ll code three simple validators, each with a different purpose related to managing restaurant reservations.

```rust
// Reservation Validator (always valid)
validator always_valid_reservation {
 spend(_customer: Option<Data>, _table: Data, _output_reference: Data, _tx: Data) {
   True
   // Reservations are always welcome!
 }
 else(_) {
   fail
 }
}
// Banned Customer Validator (always invalid)
validator banned_customer {
 spend(_customer: Option<Data>, _table: Data, _output_reference: Data, _tx: Data) {
   False
   // No service for banned patrons
 }
 else(_) {
   fail
 }
}
// Group Size Validator
validator group_size {
 spend(_customer: Option<Data>, size: Int, _output_reference: Data, _tx: Data) {
   let fits_table = size <= 8
   // Assuming maximum table size is 8
   fits_table?
 }
 else(_) {
   fail
 }
}
```
## Explaining the code:
1. always_valid_reservation
 always_valid_reservation is a simple validator that approves any spending transaction.
validator always_valid_reservation { ... }: This defines a validator named always_valid_reservation.
spend(_customer: Option<Data>, _table: Data, _output_reference: Data, _tx: Data) { ... }: This is the spend handler for the validator. It takes four arguments (all of type Data for simplicity), but it ignores them (indicated by the underscore _ prefix).
True: This line always evaluates to True, meaning this validator will always allow spending from an output locked by it.
else(_) { fail }: This is a catch-all condition, and behaves the same way to the one we described earlier. 

2. banned_customer
 banned_customer is a validator that always rejects spending transactions, simulating a ban on a customer.
validator banned_customer {: This defines a validator named banned_customer.
spend(_customer: Option<Data>, size: Int, _output_reference: Data, _tx: Data) { ... }: Similar to the previous validator, this spend handler takes four arguments but ignores them.
False: This line always evaluates to False, meaning this validator will never allow spending from an output locked by it.
else(_) { fail }: This catch-all condition ensures that only spending transactions are evaluated (and subsequently rejected).
3. group_size is a validator that only allows spending if the provided group size is 8 or less, imposing a restriction on the number of people per table.
validator group_size { ... }: This defines a validator named group_size.
spend(_customer: Option<Data>, size: Int, _output_reference: Data, _tx: Data) { ... }: This spend handler takes four arguments: an optional customer datum, an integer representing the group size, an output reference, and the transaction. It only uses the size argument.
let fits_table = size <= 8: This line checks if the size is less than or equal to 8. The result (True or False) is stored in the fits_table variable.
If fits_table is True (group size is 8 or less), the script continues. If fits_table is False (group size is greater than 8), the script fails.
else(_) { fail }: This catch-all condition handles non-spending transactions.
These examples demonstrate how Aiken can be used to define simple yet effective validators with different logic for controlling spending conditions in a smart contract. We started with these simple validators, however, in practice, you’ll likely need to implement more complex logic. 
Remember, we said validators ‘guard’ the UTxOs residing at an address. Leaving something 'unguarded', that 'always succeeds' can have dire consequences. This issue was highlighted in a high profile DDOS attack on Cardano in 2024.

## DDOS Attacker sabotages himself

Between June 24-25th 2024, Cardano was the target of a DDoS attack. The adversary executed the attack from three wallets, flooding the network with transactions containing scripts in an attempt to exhaust the network’s resources. The DDoS attack resulted in a high load on the network. Stake Pool Operators (SPOs) were negatively affected by the higher number of height battles. 

Despite these issues, the Cardano blockchain continued to operate effectively, with only minor delays in transaction processing times. The eUTxO.org explorer captured the attack visually.

**Figure 55**: eutxo.org transaction output 

The attack was halted after developers from Anastasia Labs published instructions on how to take ada from the attacker. In short, when registering a staking script, a 2 ada deposit is required by the protocol and to reclaim this deposit back, you must deregister the script. 

The attacker was complacent as no validations were guarding the 194 scripts used in the attack, so there were no restrictions on who could reclaim deposits. As each validator was written to 'always succeed', and as the transaction fee was lower than the deposit obtained, the community confiscated the adversary's ada and the attack ended. Moral of the story…keep your guard up!
