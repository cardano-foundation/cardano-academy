Anonymous functions
This code provides a set of convenient helper functions for constructing the building blocks of Cardano transactions. It makes it easier to create inputs, outputs, and addresses in Aiken.
Note that these functions are Anonymous. They are defined with the same familiar syntax, but the difference here is they are assigned to an identifier using a let-binding. This identifier is what we use to then call them later in other modules and validators.
use cardano/address.{Address, Script, VerificationKey}
use cardano/assets.{Value}
use cardano/transaction.{Datum, Input, Output, OutputReference}
pub fn input(oref: OutputReference, output: Output) -> Input {
 let input = Input { output_reference: oref, output }
 Input
}
pub fn output(address: Address, value: Value, datum: Datum) -> Output {
 let output = Output { address, value, datum, reference_script: None }
 output
}
pub fn oref(hash: ByteArray, index: Int) -> OutputReference {
 let oref = OutputReference { transaction_id: hash, output_index: index }
 oref
}
pub fn scriptAddress(hash: ByteArray) -> Address {
 let address =
   Address { payment_credential: Script(hash), stake_credential: None }
 address
}
pub fn walletAddress(hash: ByteArray) -> Address {
 let address =
   Address {
     payment_credential: VerificationKey(hash),
     stake_credential: None,
   }
 address
}
Explaining the code:
Let's break down each function line by line:
input function:
pub fn input(oref: OutputReference, output: Output) -> Input {
 let input = Input { output_reference: oref, output }
 input
}
This function creates an input object, which represents a transaction input.
It takes two arguments:
oref: An OutputReference that identifies the UTxO (Unspent Transaction Output) being consumed.
output: An Output object that represents the UTxO being consumed. This might seem redundant at first, but it's necessary because the Input object needs to contain the full details of the UTxO, not just its reference.
let input = Input { output_reference: oref, output }: This line creates the Input object by assigning the provided oref and output to its corresponding fields.
input: The function returns the created Input object.
output function:
pub fn output(address: Address, value: Value, datum: Datum) -> Output {
 let output = Output { address, value, datum, reference_script: None }
 output
}
This function creates an Output object, which represents a transaction output.
It takes three arguments:
address: An Address object that represents the recipient of the output.
value: A Value object that represents the assets being sent in the output.
datum: A Datum object that represents the optional datum attached to the output.
let output = Output { address, value, datum, reference_script: None }: This line creates the Output object with the provided values. reference_script is set to None, indicating that this output is not locked by a reference script.
output: The function returns the created Output object.
oref function:
pub fn oref(hash: ByteArray, index: Int) -> OutputReference {
 let oref = OutputReference { transaction_id: hash, output_index: index }
 oref
}
This function creates an OutputReference object, which is used to uniquely identify a UTxO.
It takes two arguments:
hash: A ByteArray that represents the transaction hash of the transaction that created the UTxO.
index: An Int that represents the output index of the UTxO within the transaction.
let oref = OutputReference { transaction_id: hash, output_index: index }: This line creates the OutputReference object.
oref: The function returns the created OutputReference object.

scriptAddress function:
pub fn scriptAddress(hash: ByteArray) -> Address {
 let address =
   Address { payment_credential: Script(hash), stake_credential: None }
 address
}
This function creates an Address object that represents a script address.
It takes one argument:
hash: A ByteArray that represents the hash of the script.
let address = Address { payment_credential: Script(hash), stake_credential: None }: This line creates the Address object. The payment_credential is set to Script(hash), indicating that this address is associated with a script. The stake_credential is set to None, as this function is creating a simple address for payment.
address: The function returns the created Address object.

walletAddress function:
pub fn walletAddress(hash: ByteArray) -> Address {
 let address =
   Address {
     payment_credential: VerificationKey(hash),
     stake_credential: None,
   }
 address
}
This function creates an Address object that represents a wallet address (an address associated with a public key).
It takes one argument:
hash: A ByteArray that represents the hash of the verification key (public key).
let address =
   Address { payment_credential: Script(hash), stake_credential: None }: This line creates the Address object. The payment_credential is set to VerificationKey(hash), indicating that this address is associated with a public key. The stake_credential is set to None, similar to the scriptAddress function previously.
address: The function returns the created Address object.
