import { Callout } from "nextra-theme-docs";
# Aiken basics

**Syntax**

Aiken code should look familiar to anyone who has coded in Rust, Gleam or Elm. Smart contracts, or validators, are based around **primitive types** built into the language: booleans, integers, strings, byte-arrays, data and void. 

These types work similarly as they do in other languages. Let’s look at ByteArrays and data. 

As the name suggests, a **ByteArray** is an array of bytes. Aiken allows you to declare a bytestring in 3 different ways, but for our example just think of it as a UTF-8 encoded byte string. Eg. “Nice burgers!”  == #[0x4e, 0x69, 0x63, 0x65, 0x20, 0x62, 0x75, 0x72, 0x67, 0x65, 0x72, 0x73, 0x21, 0x0a] 

A **Data** type can represent any user-defined type. Think of Data as a kind of wildcard, or placeholder, that can represent **any serialisable** value. Data is a special type because it is all of the types at once. In a sense, it is a super-type! Being so flexible, several Aiken builtins use Data as a way to facilitate polymorphism.

The language also includes other primitive types such as lists, tuples, options and pairs which are constructs for joining other types together. Inline comments start with //. Just add another slash, if you want to turn a comment into user-facing documentation: ///

Like most other languages, **operators** like && and || are **right-associative**, so they don't bother with their second operand if the answer is in the first one.

**Lists** are used a lot in Aiken to represent a group of elements of the same type.  

**Tuples** are similar to lists but can contain multiple different types.

Read more about the nuances of these primitives and how they work together in the *aiken-lang.org* documentation.

**Variables and Constants** 

Aiken uses let-bindings to declare variables. Remember that, like all data structures in Aiken, these variables are immutable too.

```aiken
let table_size = 8
let x = “Opening Hours:”
```

You cannot use let-bindings in a top-level module, but you can use constants to enable fixed values throughout your Aiken project.
```aiken
const closing_time = 2200
const open_at_weekend = False
```
Note that constants can contain any arbitrary computation. So, for example, 
```aiken
const two = 1 + 1
```
…is perfectly valid in Aiken, and bears no runtime difference with:
```aiken
const two = 2
```
It is best practice, even though optional, to use type annotations with variables and constants to aid readability.
```aiken
const name : ByteArray = "I can Aiken"
const restaurant_capacity : Int = 200
```
**Functions**

You might hear it said that functions are a first class citizen in Aiken. This basically means they are given priority treatment. You can assign them to variables, pass them to other functions, or do most other things you would do with a supported data type. 

```aiken
/// A function taking another function as an argument

fn cook_twice(f: fn(chips) -> chips, x: chips) -> chips {
  f(f(x)) // twice-cooked chips
}

fn add_one(x: Int) -> Int {
  x + 1
}

fn add_two(x: Int) -> Int {
  cook_twice(add_one, x)
}
```
**Blocks**

Most things, including blocks, are evaluated as an expression in Aiken. Each expression in the block is executed, but it’s only the result of the last expression that is returned.

```aiken
let value: Bool = {
   "Welcome!"
   200 + 1
   True
}
value == True
```
**Recursion**

Remember Aiken is a functional programming language, so it doesn't have control flow for loops. Instead, it relies heavily on **recursion**. Think of a recursive function as a function that solves a problem by solving smaller instances of the same problem. Recursion is a powerful feature in an execution environment like Plutus on Cardano. Let’s look at a simple recursive function.

```aiken
/// Calculates the total number of ways to arrange pineapple slices on a pizza.
/// If you have 'n' pineapple slices, this function calculates how many different ways
/// you can arrange them on your pizza.
/// For example, with 3 slices, you could have:
///  - slice1, slice2, slice3
///  - slice1, slice3, slice2
///  - slice2, slice1, slice3
///  ..etc...giving a total of 6 possible arrangements (3! = 3 * 2 * 1 = 6)

pub fn pineapple_arrangements(n: Int) -> Int {
  if n <= 1 {
    // Base case: with 0 or 1 slice, there's only 1 arrangement
    1
  } else {

   // Recursive case: n! = n * (n-1)!
   n * pineapple_arrangements(n - 1)
 }
}

test no_pineapple_one_arrangement() {
   pineapple_arrangements(0) == 1
}

test one_pineapple_one_arrangement() {
   pineapple_arrangements(1) == 1
}

test three_pineapple_six_arrangements() {
   pineapple_arrangements(3) == 6
}

test pineapple_slices6() {
   pineapple_arrangements(6) == 720
}

test should_fail_pineapple_slices() {
   pineapple_arrangements(6) == 72
}
```

**Tracing**

Most of our Aiken code is written as **predicates**, functions that return ```True``` or ```False``` and nothing else. It’s a black and white, yes or no response to whether an operation is allowed or not. This is a good thing. It promotes determinism, or predictability, for everyone. This is what we want when transferring potentially large amounts of value! 

This is all fine, but in large programs, it can be tough to see the woods from the trees, as nearly all outputs are just ```True``` or ```False``` boolean results. To help troubleshoot, Aiken allows you to add **traces** that tell the compiler to turn on log messaging for this expression, or predicate. If there is an issue, we can follow up by inspecting the log messages encountered during execution. It’s best practice to add a string comment for readability. Use the format: @ “message” 

```aiken
fn under_capacity(n: Int) -> Bool {
   trace @"under_capacity"
   n < 200 == True
}

fn full_up(n: Int) -> Bool {
   trace @"full_up"
   n >= 200
}
```
We’ll look at more involved examples later. We just wanted to introduce the concept for now. There is more detail in the Aiken documentation.[^1]


[^1]: Aiken documentation, aiken-lang.org/language-tour/troubleshooting#traces
