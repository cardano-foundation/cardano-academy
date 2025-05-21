On Cardano, outputs in the UTxO model have an address and a value. The address decides who is allowed to spend this output. This contains a PubKey Hash, the hash of a verification key. Any transaction wishing to spend the output must be signed by the corresponding signing key, but the transaction may require signing by multiple keys. 

UTxOs are like vouchers in that they are independent, immutable and can be spent only once – and only in their entirety. Like vouchers, UTxOs are disposable objects. When a transaction is submitted, it refers to one or more UTxOs as its inputs, which are to be consumed. When an input UTxO is spent, it results in the creation of one or more new UTxOs. 

Cardano transactions must balance. What does that mean? Usually, the sum of input values must equal the sum of output values. Exceptions include the following:

- A transaction needs to cover transaction fees. Usually, they get taken from the inputs before comparing them to the outputs.
- Cardano transactions can mint, or burn, native assets.
- Staking rewards need to be withdrawn. This is a special case where rewards are added to the outputs without having compensating inputs. Note that Cardano uses a Chimeric Ledger in which reward accounts are distinct from UTxOs and are more akin to accounts in account-based blockchains. They are used for accumulating staking rewards, rather than using UTxOs. This is in order to avoid creating a large number of UTxOs with tiny values. Cardano creates a reward account automatically when a staking credential is registered. Each reward account links to a staking credential, and users cannot create them arbitrarily. 

Like real life, it’s often the case that you don’t have the exact change. In this case one or more transaction outputs go back to you as change. These are called **change outputs**. You can make up the price any way you wish: with a chunk of UTxOs, coins or vouchers using our analogy.  

This may sound like a headache. But in practice, wallets take care of this for the user. The wallet software creates transactions automatically using the right amount of UTxOs as inputs and creating the correct outputs.

When you are paying, you don’t want too many UTxOs in your wallet. You would also prefer not to get back too many small UTxOs as change. Wallets try to strike a balance between these competing goals. This process of picking the correct inputs is a field of study in its own right, called **coin selection**.

There is even a Cardano Improvement Proposal on the topic, CIP-002 Coin Selection Algorithms for Cardano.[^1] The community has tried various solutions. One, UnFrack.it, attempts *'to modify and optimize your (Cardano) wallet so you get cheaper transactions and fewer errors.'* Cardano also has a ‘minADA’ requirement of 1 ADA per UTxO which mitigates the build up of too many tiny UTxOs, aka UTxO dust. 

Network latency means the transition to a new state across all network nodes is progressive. This is the same challenge facing all blockchains. On the Cardano network, a node produces a new block, initiating the transition to a new state. This transition only ends when all nodes have received this block. If the block is valid, and thus accepted by all nodes, a state transition takes place, accompanied by a change of state.   

**Figure 20:**   UTxO state transitions  

[^1]: CIP-0002 Coin Selection Algorithms for Cardano, cips.cardano.org/cip/CIP-0002
