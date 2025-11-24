# Storage Requirements: UTxO vs Account Model

The account model is commonly thought to be more efficient than UTxO in terms of memory usage. There are fewer storage demands for storing a single account balance when compared to storing the UTxOs that make up a user's balance. Transactions in the account model are generally smaller in size because they only require the sender, receiver, transfer amount and just one digital signature.

If you look at the bare stats, however, there appears to be more nuance. Ethereum requires wallets to download over a terabyte of data to sync, and the Solana blockchain has bloated to 3.8 terabytes. Cardano compares favorably at 180 GB at time of writing. 

We will see later how Cardano’s Extended UTxO model allows for most of the computation to take place off-chain, and a single transaction can include many transactions, scripts and assets. With UTxO, a single transaction can consume and produce a huge amount of inputs and outputs respectively. You can inspect record transactions and block stats at eutxo.org.

Meanwhile Ergo, another EUTxO-based blockchain, has already produced 5,000 outputs in a single transaction. So it is fair to say comparing account-based transactions with eUTxO transactions is not an apples to apples comparison.

## Questions

Which blockchain has experienced significant bloat in its storage requirements?

A. Bitcoin
B. Cardano
C. Ethereum
**D. Solana**
