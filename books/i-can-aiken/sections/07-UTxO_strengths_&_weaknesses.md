**UTxO strengths**

UTxOs can be validated in parallel. This can potentially improve transaction processing efficiency and scalability. While not completely private, the UTxO model also offers some privacy benefits as it enables users to generate new addresses for each transaction, making it tricky to link transactions to a single identity.

**Security** 

Security is arguably Bitcoin’s best selling point and the reason many see it as a store of value and hedge against inflation. For example, the UTxO model prevents double-spending: each UTxO can be spent only once, and the network verifies that inputs are indeed unspent. 

**UTxO weaknesses**

Compared to account-based systems, the UTxO model is non-trivial to understand and design for. Some developers have reported that implementing complex smart contracts using the UTxO model is more challenging than with account-based models. 

Bitcoin Transactions can create tiny UTxOs, known as **dust**, that can quickly clog up a wallet and make it uneconomical to form transactions. As mentioned above, Bitcoin does offer some privacy, but a determined actor can leverage chain analysis techniques to trace transactions and potentially link them to real-world identities.

**Analogy**

UTxO is often explained as **cash in cash out**. Let's say you are paying your bill at a restaurant using the UTxO model. The transaction is stateless and deterministic. You and the waiter don’t care how busy other restaurants are, or if other payment systems are slow. Once you are both happy with the terms, the transaction can proceed with deterministic predictability. The bill is $40, so you pay $50, leave a tip of $5, and receive $5 change back. Inputs ($50) = outputs ($40 bill + $5 tip + $5 change). 


**Figure 6:**  ‘Cash in cash out’ analogy

Consider each bill to be a UTxO which must be spent in its entirety. You also could have paid four separate $10 bills, or four UTxOs and received nothing back. The restaurant next door, indeed any restaurant anywhere, could also be taking payments in parallel using the UTxO model, unaffected and oblivious to your transaction. The success or failure of the transaction depends on the transaction itself and its inputs. Since no external factors are involved, transactions can be evaluated in isolation. Of course, there may be many UTxOs transferring about the blockchain that, in the context of our ‘local’ transaction, we don’t need to care about. 

The cash analogy is simple and intuitive but it is not completely accurate. While you must spend complete UTxO’s, or dollar bills, you can also create new UTxOs with arbitrary values. Obviously if you pay your bill with cash, you can’t just create new dollar bills out of thin air. With the UTxO model, however, you can create new UTxOs with arbitrary values–provided of course they do not exceed the total value of the UTxO(s) you spend. Another flaw in the analogy is that the UTxOs consumed are spent and removed from the UTxO set after a transaction, while cash continues in circulation. 

A more appropriate analogy is to pay in vouchers. You can pay your bill using voucher(s) of nominal value. These vouchers are consumed, or redeemed, and are of no use after the transaction. Once they cover the bill, you could pay the waiter using one or multiple vouchers and receive voucher(s) back as change. 

We’ll revisit the UTxO model later in much more depth. For now, let's jump forward a few years to talk about **Bitcoin Script**.
