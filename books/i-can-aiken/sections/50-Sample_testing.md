# 50. Sample testing 

For each validator we code, we should write some tests. The following code defines a test case for the ```validate_reservation``` validator we discussed earlier. Taking a closer look...

```aiken
use aiken/interval.{Finite, Interval, IntervalBound}
use arrive_on_time/arrive-on-time
use cardano/transaction.{Transaction, placeholder}
use tests/anonymous as t
use types/arrive_on_time.{ReservationDetails}
test arrive_on_time_validator() {
 let r = Void
 let customerId = #"face"
 let oref = t.oref(#"dead", 1)
 let reservationDetails =
   ReservationDetails { reserved_for: customerId, reservation_expiry: 1000 }
 let tx =
   Transaction {
     ..placeholder,
     extra_signatories: [customerId],
     validity_range: Interval(
       IntervalBound { bound_type: Finite(0), is_inclusive: True },
       IntervalBound { bound_type: Finite(1000), is_inclusive: True },
     ),
   }
 arrive-on-time.validate_reservation.spend(Some(reservationDetails), r, oref, tx)?
}
```

## Explaining the code:

Lines 1-10: Setup and Imports

- ```use aiken/interval.{Finite, Interval, IntervalBound}```: This imports types related to time intervals from the ```aiken/interval``` module. These are used to define the validity range of the transaction.

-  ```use arrive_on_time/arrive-on-time```: This imports the ```arrive-on-time``` module.

- ```use cardano/transaction.{Transaction, placeholder}```: This imports the ```Transaction``` type and a ```placeholder``` function from the ```cardano/transaction``` module. The ```placeholder``` function helps create a dummy transaction for testing.

- ```use tests/anonymous as t```: This imports a module named ```anonymous.ak``` from the ```tests``` directory and aliases it as ```t```. This is the module we coded earlier which contains anonymous functions.

- ```use types/arrive_on_time.{ReservationDetails}```: This imports the ```ReservationDetails``` type, which holds the reservation information.

Lines 12-31: Test Case Definition

- ```test arrive_on_time_validator() {```: This defines a test function named ```arrive_on_time_validator```.

Lines 13-15: Variable Initialization

- ```let r = Void```: This initializes a variable ```r``` with the Void type, indicating an empty redeemer.

- ```let customerId = #"face"```: This sets a variable ```customerId``` to a byte string value #"face". This represents the ID of the customer making the reservation.

- ```let oref = t.oref(#"dead", 1))```: This creates an ```OutputReference``` using an anonymous function ```t.oref``` from the ```tests/anonymous``` module. This is a dummy output reference for testing purposes.

Lines 17-19: Reservation Details

- ```let reservationDetails =  ReservationDetails {  ... }```: This creates a ```ReservationDetails``` value with the following information:
   - ```reserved_for: customerId```: The reservation is for the customer with ID #"face".
   - ```reservation_expiry: 1000```: The reservation expires at time 1000.

Lines 21-30: Transaction Construction

- ```let tx = Transaction { ... }```: This creates a Transaction value with the following details:
    - ```..placeholder```: This  fills in the remaining fields of the transaction with default or placeholder values.
    - ```extra_signatories: [customerId]```: The transaction is signed by the customer with ID ```#"face"```
    - ```validity_range: Interval(...)```: This defines the validity range of the transaction as an interval from time 0 to 1000, inclusive.

Line 31: Validator Execution

- ```arrive-on-time.validate_reservation.spend(Some(reservationDetails), r, oref, tx)?```: This line executes the ```spend``` handler of the ```validate_reservation``` validator with the following arguments:
      - ```Some(reservationDetails)```: The datum containing the reservation details.
      - ```r```: The redeemer (which is ```Void``` in this case).
      - ```oref```: The output reference.
      - ```tx```: The transaction.

Aiken has its own built-in **property-based testing** framework with **integrated shrinking**. While the unit tests we ran earlier check that the output is identical to a pre-computed expected result, property-based tests check properties. Property-based test cases explore possible inputs looking for behaviour patterns rather than specific cases.

**Integrated shrinking** is a feature of property-based testing that simplifies failing test cases. It's ‘integrated’ because the shrinking process is tightly coupled with the generation of test data. When a test fails, the integrated shrinking feature automatically simplifies the data, bit by bit, until it finds the smallest piece that still causes the problem. It is more efficient this way as it allows for the precise identification of the issue directly. The Aiken property-based testing framework integrates and automatically manages this process for you.

For our simple example, we’ll use a property-based test with a single argument that specifies a ```Fuzzer```. A fuzzer generates random values for our stress test. This ```aiken/fuzz``` library takes care of generating the pseudo-randomness for you, allowing you to write fuzzers using a simple via keyword. Just make sure you have the right syntax. It must be of type ```Fuzzer<a>```, so in our example we are using type ```Fuzzer<Int>```. 

```aiken
use aiken/fuzz
test restaurant_under_capacity(n: Int via fuzz.int()) {
 n <= 300
}
```
Similar to unit tests, property-based tests are run with the aiken check command. The report returned highlights the number of random samples checked and a simple counterexample if the test fails. This was obviously a simple example, check the documentation for more complex scenarios.

**Figure 54**: sample ```aiken check``` output 
