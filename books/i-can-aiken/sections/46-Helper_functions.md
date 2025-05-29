46. Helper functions
Let's write some more code. To keep it simple, we’ll continue with our restaurant analogy for the validators we’re about to code. Understand, however, that many of the checks and conditions are similar to those found in any context. For example, we’ll be checking UTxO inputs are indeed unspent, time intervals are valid, required signatures are present. 

Following best practice, we will write our validators in the validators folder. But first let's create some supporting functions in the lib folder. We’ll use .ak as the file extension throughout. We’ll explain different features as we go. It may seem overwhelming at first, but, as we write more validators, you will see a lot of the similar functionality. For brevity, we’ll explain things once, so feel free to skip back and forth, or, of course, refer to the docs on the Aiken-lang.org website.

Aiken code comprises functions and types bundled together in modules. Each module can export types and values for use by other modules in the project. We’ll follow the standard practice of having all the modules for our project reside within a directory with the same name as the project.

This code defines helper functions and test cases for managing restaurant reservations. The helper functions ensure that the reservation is used by the correct person and within the valid time frame. The subsequent test cases help verify the logic of the must_dine_before_expiry function.
use aiken/collection/list
use aiken/interval.{Finite, Interval}
use cardano/transaction.{ValidityRange}
//helper function to check if the diner matches the reservation
pub fn must_be_dined_by(diners, reserved_for) -> Bool {

  // Check if the reserved customer is in the list of diners
  list.has(diners, reserved_for)
}

// helper function to check if the dining time is within valid reservation
pub fn must_dine_before_expiry(
  range: ValidityRange,
  reservation_expiry: Int,
) -> Bool {
 when range.lower_bound.bound_type is {
   // If the earliest time is finite, check if it's before the expiry
   Finite(dining_start_time) -> dining_start_time <= reservation_expiry
   // Else, the lower bound is infinite, so we fail
   _ -> False
 }
 //if the dining time is not specified, it's invalid
}

// These tests are for ensuring the logic of the helper functions are ok
test early_dining_is_valid() {
 must_dine_before_expiry(interval.after(2), 3)
 // dining starts at time 2, expiry is at time 3
}

test dining_on_time_is_valid() {
  must_dine_before_expiry(interval.after(2), 2)
  // dining starts at time 2, expiry is also at time 2
}

test late_dining_is_invalid() {
  !must_dine_before_expiry(interval.after(3), 2)
  // dining starts at time 3, expiry is at time 2
}
Explaining the code:

Import the necessary modules with the ‘use’ keyword:
use aiken/collection/list: Provides functions for working with lists, used for checking if an element is in a list.
use aiken/interval.{Finite, Interval}: Imports types for working with time intervals:
Finite: Represents a finite bound in a time interval.
Interval: Represents a time interval with a lower and upper bound.
use cardano/transaction.{ValidityRange}: Imports the ValidityRange type, which defines the time range during which a transaction is valid. This is used to represent the time of a dinner reservation.
We use the fn keyword to define functions in Aiken. Functions can take arguments, or typed arguments, and always have a return type. Everything in Aiken is an expression, so you won't see a return keyword in any function, they just return whatever they evaluate to.
fn add(bill: Int, tip: Int, change: Int) -> Int {
  bill + tip + change
}

fn multiply(rating: Int, stars: Int) -> Int {
  rating * stars
}
These functions are private, so they can only be called by other functions within the same module. If we use pub keyword, it makes them usable in other modules.
pub fn must_be_dined_by(diners, reserved_for) -> Bool {
   // Check if the reserved customer is in the list of diners
   list.has(diners, reserved_for)
}
This defines a helper function must_be_dined_by that checks if a reservation is being used by the person it was reserved for.
diners: Represents a list of people who are dining.
reserved_for: Represents the person for whom the reservation was made.
list.has(diners, reserved_for) This uses the list.has function to check if the reserved_for person is present in the diners list. It returns True if found, False otherwise.
Lists are used a lot in Aiken. Think of them as ordered collections of elements, all of which must be of the same type. Remember that all data structures in Aiken are immutable, so adding an element to a list creates a new list. The old list remains unchanged. 
// helper function to check if the dining time is within valid reservation
pub fn must_dine_before_expiry(
 range: ValidityRange,
 reservation_expiry: Int,
) -> Bool {
 when range.lower_bound.bound_type is {

   // If the earliest time is finite, check if it's before the expiry
   Finite(dining_start_time) -> dining_start_time <= reservation_expiry

   // Else, the lower bound is infinite, so we fail
   _ -> False
 }
 //if the dining time is not specified, it's invalid
}
This defines another helper function must_dine_before_expiry that checks if a reservation is being used before its expiry time.
range: A ValidityRange representing the time range during which the reservation is valid.
reservation_expiry: An Int represents the expiry time of the reservation.
when range.lower_bound.bound_type is { ... }: 
 
For nameless fields in Aiken, we use the when *expr* is keywords for pattern-matching. As the documentation advises, it is like asking the compiler 'If the data has this shape then do that' for all possible shapes.  

In this case, we use pattern-matching to check the type of the lower bound of the validity range. 
Finite(dining_start_time) -> dining_start_time <= reservation_expiry: If the lower bound is Finite, it extracts the earliest valid time (dining_start_time) and checks if it's less than or equal to the reservation_expiry.
_ -> False: In any other case (for example, if the lower bound is infinite), the function returns False, indicating the reservation is not valid.

Unit-test and property-based testing is easy with Aiken.

Before we compile our code, we can check for bugs. Aiken has built in support for tests. What does that mean? It means we can write tests in our code, and easily check them with aiken check, which returns some useful stats in a short report. They work similarly to functions that take no arguments and have to return a Bool. A valid test returns True, and, if it fails, False. It can also return Void. This is a more recent addition but tests may also simply return Void, in which case they are considered successful if they don't fail.

Tests can use any function, constant or types defined in a module, but note that tests cannot reference other tests. One key feature we alluded to earlier in the course is that tests run on the same virtual machine which runs validators on-chain. In other words, we can assume the tests are accurately mirroring how the code will run in production.
// These tests are for ensuring the logic of the helper functions are ok
test early_dining_is_valid() {
 must_dine_before_expiry(interval.after(2), 3)
 // dining starts at time 2, expiry is at time 3
}
This is a test case that checks if the must_dine_before_expiry functions correctly, handling a valid scenario where the dining time is before the reservation expiry. interval.after(2) creates a ValidityRange that starts at time 2, and the expiry time is set to 3. The test expects this to return True.
test dining_on_time_is_valid() {
  must_dine_before_expiry(interval.after(2), 2)
  // dining starts at time 2, expiry is also at time 2
}
This test case checks if the function correctly handles a scenario in which the dining time is exactly at the reservation expiry time. It also expects this to return True.
test late_dining_is_invalid() {
 !must_dine_before_expiry(interval.after(3), 2)
 // dining starts at time 3, expiry is at time 2
}
This test case checks if the function correctly handles an invalid scenario in which the dining time is after the reservation expiry. It uses the ! operator to negate the result, expecting it to return False.

Running aiken check returns a report that requires the memory and CPU execution units for each test. This allows us to use tests to benchmark different versions of our code. It grants us some flexibility also, as there’s no real execution limit as seen on-chain. 

This code defines helper functions for our tipping and customer review system. The functions do the following: 
Ensure that the tip amount is above a minimum threshold
count script inputs in a transaction
verifies the integrity of the data by checking if the owner remains the same and if new reviews are correctly appended to the existing ones.
use aiken/collection/list
use cardano/address.{Script}
use cardano/transaction.{Input}
use types/tipping.{Datum}

// Helper Functions

// Minimum tip amount (like a suggested gratuity)
pub const minimum_tip: Int = 5000000

// Count script inputs
pub fn count_input_scripts(inputs: List<Input>) -> Int {
 list.count(
   Inputs,
   fn(input) {
     when input.output.address.payment_credential is {
       Script(_) -> True
       _ -> False
     }
   }
 )
}

// Verify data integrity

pub fn datum_is_correct(inputDatum: Datum, outputDatum: Datum) -> Bool {
 and {
   inputDatum.owner == outputDatum.owner,
   datum_contains_one_more_reviews(inputDatum.reviews, outputDatum.reviews)?,
 }
}

// Ensure reviews are appended

pub fn datum_contains_one_more_reviews(
 input_reviews: List<ByteArray>,
 output_reviews: List<ByteArray>,
) -> Bool {
 let new_message = list.head(output_reviews)
 when new_message is {
   Some(msg) -> list.push(input_reviews, msg) == output_reviews
   None -> False
 }
}
Explaining the code:

Import necessary modules with the ‘use’ keyword:
use cardano/address.{Script}: Imports the Script type, representing a Plutus script, used to identify script inputs.
use cardano/transaction.{Input}: Imports the Input type, representing a transaction input, used to analyze inputs to a script.
use types/tipping.{Datum}: We can import types from another module with the ‘use’ keyword. This line imports the Datum type from a custom module types/tipping. This type holds data related to tipping, such as the recipient and the tip amount.
// Helper Functions
// Minimum tip amount (like a suggested gratuity)
pub const minimum_tip: Int = 5000000
This line defines a public constant minimum_tip and sets its value to 5000000. This constant represents the minimum amount of Lovelace (ADA) required for a tip. In the last piece of code, we mentioned how the pub keyword can make modules reusable by other modules in the project. This pub keyword works similarly for Functions, type-aliases and constants. It exports them from a module, making them available for other functions. Otherwise they are considered private.
// Count script inputs

pub fn count_input_scripts(inputs: List<Input>) -> Int {
 list.count(
   Inputs,
   fn(input) {
     when input.output.address.payment_credential is {
       Script(_) -> True
       _ -> False
     }
   },
 )
}
This defines a function count_input_scripts that counts the number of script inputs in a transaction.
inputs: A list of transaction inputs (List<Input>).
list.count(inputs, fn(input) { ... }): This uses the list.count function to count the elements in the inputs list that satisfy a certain condition.
The condition is defined by an anonymous function (fn(input) { ... }) that checks if the payment_credential of the input's address is a Script. If it is, the function returns True, indicating that this input is a script input.
Anonymous functions are defined with the same familiar syntax but assigned to an identifier using a let-binding. This identifier, ‘input’ in this case, is the name called elsewhere. We will define this ‘input’ anonymous function shortly. 

Note the use of the _ wildcard here. We need to always complete patterns, but accounting for every single field or constructor can be tedious or just not possible. Aiken has you covered here. You can just use a _ wildcard which you can think of as a fallback pattern. Stick it in there as a kind of placeholder to match any remaining patterns. 

We just use the wildcard _ on its own here, but we could give it a name. We’ll also see later that any identifier starting with _ is treated as a wildcard. It’s best practice to use wildcards only as a last resort, because they can make your code age poorly! It is usually better to list all patterns explicitly with a when *expr* is clause, for example. 
// Verify data integrity
pub fn datum_is_correct(input_datum: Datum, output_datum: Datum) -> Bool {
 and {
   input_datum.owner == output_datum.owner,
   datum_contains_one_more_reviews(input_datum.reviews, output_datum.reviews)?,
 }
}
This defines a function datum_is_correct that checks if the data in the output datum is a valid update from the input datum.
input_datum: The datum from the input UTxO.
output_datum: The datum from the output UTxO.
and { ... }: This combines two conditions using the and operator. Both conditions must be True for the function to return True.
input_datum.owner == output_datum.owner: Checks if the owner field in both datums is the same.
datum_contains_one_more_reviews(input_datum.reviews, output_datum.reviews)?: Calls the datum_contains_one_more_reviews function to check if the reviews list in the output datum has exactly one more review than the input datum. 
Note our first encounter with the ? operator here, which means 'trace-if-false operator'. What does it do exactly? Good question.

Most of what we’re looking at in these validators are just predicates. Or, in simple terms, functions that return either True or False. We’ll see as we write more validators that there can be a lot of booleans expressions AND’d or OR’d together. In amongst hundreds or thousands of lines of code, it’s easy to quickly lose sight of the original context or intent. For example, take the following: 
let pizza_must_be_edible = True
let !pineapple_on_pizza = False
pizza_must_be_edible && !pineapple_on_pizza
This returns False, but just False, so it’s easy to lose track of which branch was False in the original code. What if we need to troubleshoot much larger expressions?

The ? in the code is a postfix operator we can add to any boolean expression. It instructs the compiler to trace the expression only if it evaluates to False. This is really helpful to inspect an entire evaluation path that returned the False. So we could have coded above:
pizza_must_be_edible? && !pineapple_on_pizza?
Which would have created the trace !pineapple_on_pizza ? False.
The ? operator behaves like trace, in that it’s affected by the Also at compile time, it has no impact on the code and the compiler ignores it.
// Ensure reviews are appended
pub fn datum_contains_one_more_reviews(
 input_reviews: List<ByteArray>,
 output_reviews: List<ByteArray>,
) -> Bool {
 let new_message = list.head(output_reviews)
 when new_message is {
   Some(msg) -> list.push(input_reviews, msg) == output_reviews
   None -> False
 }
}
This defines a function datum_contains_one_more_reviews that checks if the output_reviews list contains all the elements from the input_reviews list plus one new element at the beginning.
input_reviews: The list of reviews from the input datum. 
output_reviews: The list of reviews from the output datum.
let new_message = list.head(output_reviews): This gets the first element (head) of the output_reviews list.
when new_message is { ... }: This uses pattern matching to handle the case where the output_reviews list is not empty.
Some(msg) -> list.push(input_reviews, msg) == output_reviews: If there is a new message (msg), it appends this message to the input_reviews list and checks if the result is equal to the output_reviews list.
None -> False: If the output_reviews list is empty, the function returns False.
This code defines two helper functions for a rewards points system. The points_earned function checks if a member is eligible for rewards by verifying their ID against a list of valid members. The points_sufficient function checks if a member has accumulated enough reward points to claim a reward.
use aiken/collection/list
use aiken/interval.{Finite}
use cardano/transaction.{ValidityRange}
use types/vesting.{MemberIDHash, RewardPoints}

// Check if the member's ID matches the one on file
pub fn points_earned(tx_signatures: List<MemberIDHash>, member_id: MemberIDHash) {
 list.has(tx_signatures, member_id)?
 // Is their ID on the list of valid members?...trace if fail
}

// Check if enough points have been accumulated
pub fn points_sufficient(range: ValidityRange, required_points: RewardPoints) {
 when range.upper_bound.bound_type is {
   Finite(total_points_earned) -> (required_points <= total_points_earned)?
   // Enough points? ...trace if fail
   _ -> False
 }

 // Not enough
}
Explaining the code:

Import necessary modules with ‘use’ keyword:
use aiken/collection/list: Provides functions for working with lists, specifically used here for checking membership in a list.
use cardano/transaction.{ValidityRange}: Imports the ValidityRange type, used here to represent a range of reward points.
use types/vesting.{MemberIDHash, RewardPoints}: Imports two custom types from a module named types/vesting:
MemberIDHash:  represents a hash of a member's ID.
RewardPoints:  represents a quantity of reward points.
// Check if the member's ID matches the one on file
pub fn points_earned(tx_signatures: List<MemberIDHash>, member_id: MemberIDHash) {
 list.has(tx_signatures, member_id)?
 // Is their ID on the list of valid members?
}


This defines a function points_earned that checks if a given member ID is present in a list of valid member IDs.
tx_signatures: A list of MemberIDHash values represent the IDs of members who have signed a transaction.
member_id: A MemberIDHash value representing the ID of the member whose points are being checked.
list.has(tx_signatures, member_id): This uses the list.has function to check if the member_id is present in the tx_signatures list. It returns True if the ID is found, and False otherwise.
// Check if enough points have been accumulated
pub fn points_sufficient(range: ValidityRange, required_points: RewardPoints) {
 when range.upper_bound.bound_type is {
   Finite(total_points_earned) -> (required_points <= total_points_earned)?
   // Enough points?
   _ -> False
 }
 // Not enough
}
This defines a function points_sufficient that checks if the total points earned are greater than or equal to the required points for a reward.
range: A ValidityRange value represents the range of earned reward points.
required_points: A RewardPoints value represents the number of points required to claim a reward.
when range.upper_bound.bound_type is { ... }: This uses pattern-matching to check the type of the upper bound of the ValidityRange.
Finite(total_points_earned) -> (required_points <= total_points_earned)?: If the upper bound is Finite, it extracts the value of the upper bound (total_points_earned) and checks if it's greater than or equal to required_points. 
_ -> False: If the upper bound is not Finite (if it's infinite), the function returns False, indicating there are not enough points.
