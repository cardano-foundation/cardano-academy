```aiken
use aiken/collection/list
use aiken/crypto.{VerificationKeyHash}
use cardano/assets.{AssetName, PolicyId, quantity_of}
use cardano/transaction.{OutputReference, Transaction}

validator token_gate(
  owner: VerificationKeyHash,
  policy: PolicyId,
  name: AssetName,
) {
  spend(
    _datum: Option<Data>,
    _redeemer: Data,
    _own_ref: OutputReference,
    self: Transaction,
  ) {
    // Check 1, identity: the owner signed this transaction.
    let signed = list.has(self.extra_signatories, owner)
    // Check 2, proof: some reference input carries the token.
    // Read, not spent — CIP-31.
    let proven = list.any(
      self.reference_inputs,
      fn(input) { quantity_of(input.output.value, policy, name) >= 1 },
    )
    signed && proven
  }

  else(_) {
    fail
  }
}


```
