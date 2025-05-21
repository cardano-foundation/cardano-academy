There are trade-offs for both the UTxO and the account model when it comes to privacy.

You can’t link transactions straightforwardly with UTxO, because you can constantly use new addresses for each transaction. Chain analysis tools are required to track ownership of UTxOs. In contrast, many feel the account model provides greater fungibility. Remember fungibility is a property of digital assets whose units are interchangeable. 

Fungibility is important in terms of preserving censorship resistance and privacy. A single balance updates when several transactions top up an Ethereum account . When this account makes a subsequent payment, an observer cannot determine which funds are being spent. That said, the account model reuses addresses, which makes a clear transaction history possible, like a traditional bank account.  

While there are examples of 'coin mixers' on Ethereum,[^1] eUTxO blockchain Ergo also offers  ErgoMixer,[^2] 'a web application for mixing ergs and tokens based on the Ergo platform.' 

[^1]: Ethereum ‘coin mixer’, ethereum-mixer.io/
[^2]: ErgoMixer, github.com/ergoMixer/ergoMixBack
