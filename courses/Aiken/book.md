```aiken
use aiken/collection/list
use aiken/crypto.{VerificationKeyHash, blake2b_256}
use cardano/transaction.{OutputReference, Transaction, placeholder}

/// Who may claim, and the sealed case file they must match
pub type Datum {
  /// The only key allowed to claim the locked funds
  owner: VerificationKeyHash,
  /// Commitment: the hash of the claimant's name
  case_file: ByteArray,
}

pub type Redeemer {
  /// The name whose hash must match the case file
  name: ByteArray,
}

/// The rule the judge applies, as a plain testable function
pub fn can_claim(d: Datum, r: Redeemer, self: Transaction) -> Bool {
  and {
    (blake2b_256(r.name) == d.case_file)?,
    list.has(self.extra_signatories, d.owner)?,
  }
}

validator case_closed {
  spend(
    datum: Option<Datum>,
    redeemer: Redeemer,
    _utxo: OutputReference,
    self: Transaction,
  ) {
    when datum is {
      Some(d) -> can_claim(d, r: redeemer, self: self)
      // the r: and self: labels name the arguments at the call site; Aiken lets you label arguments for readability
      None -> False
    }
  }

  else(_) {
    fail
  }
}

// --- Tests: same file, same virtual machine as on-chain ---
const owner = #"00000000000000000000000000000000000000000000000000000abc"

const stranger = #"00000000000000000000000000000000000000000000000000000def"

fn locked_for(name: ByteArray) -> Datum {
  Datum { owner, case_file: blake2b_256(name) }
}

fn signed_by(key: VerificationKeyHash) -> Transaction {
  Transaction { ..placeholder, extra_signatories: [key] }
}

test right_name_right_signature_claims() {
  can_claim(
    locked_for("Ada Lovelace"),
    Redeemer { name: "Ada Lovelace" },
    signed_by(owner),
  )
}

test wrong_name_cannot_claim() fail {
  can_claim(
    locked_for("Ada Lovelace"),
    Redeemer { name: "Lord Byron" },
    signed_by(owner),
  )
}

test strangers_cannot_claim_even_with_the_name() fail {
  can_claim(
    locked_for("Ada Lovelace"),
    Redeemer { name: "Ada Lovelace" },
    signed_by(stranger),
  )
}


```
