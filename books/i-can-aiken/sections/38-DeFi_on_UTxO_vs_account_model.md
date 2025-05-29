**DeFi_on_UTxO_vs_account_model**

Decentralized finance, **DeFi**, relies heavily on lending protocols that allow users to lend and borrow crypto assets without intermediaries. The underlying account model influences the design and functionality of these protocols. Borrowers typically use their crypto assets as collateral, which the protocol holds until the loan is repaid. Lenders can earn interest on their assets.  

For example, if two users deposit ada and USDM (Moneta stablecoin), they can borrow each other's assets. To minimize risk, borrowers often provide more collateral than the loan amount. This is known as over-collateralization. The required **over-collateralization** ratio depends on the volatility of the collateral. Some platforms also offer uncollateralized flash loans that must be repaid immediately. 

In DeFi lending, agreements are written as **smart contracts** that remove the need for intermediaries and increase trust. Borrowers must provide collateral greater than the loan value to reduce default risk. This collateral is held securely and can be liquidated if the borrower fails to repay. **Interest rates** are set automatically based on market dynamics, ensuring competitive rates. Lenders deposit assets into **liquidity pools**, making funds readily available for borrowers. This pooling system enhances liquidity and ensures sufficient funds for lending. 

UTxO and Account-based models offer distinct pros and cons for lending. Developers need to understand these differences to create effective protocols.

The **Account model**, such as the one used in Ethereum, manages all funds under a single contract address. This has some key benefits. Firstly, it is more intuitive for developers, as it simplifies how the system keeps track of balances and manages state. This makes complex financial operations easier to develop. Secondly, managing all funds under one address is more intuitive to implement. However, there's a security risk: if this central contract is compromised, users could lose their assets.

In contrast, the **UTxO model** spreads funds across individual user UTxOs. This decentralized approach offers unique advantages. State management is distributed, with each user validating changes. This increases security but also makes it more challenging to form liquidity pools. To overcome this, a UTxO may use 'locks' to secure the distributed funds and enforce rules during transactions. These locks function similarly to validators. Since it is the users, not a contract, who directly control their assets, security is enhanced. Even if a contract fails, users retain control of their assets. 

Lending protocols on **Cardano** need to work around the fact that UTxOs are distributed. To do this, developers create validator scripts to manage and combine users' funds. These scripts contain the business logic for rules, such as price conditions, to ensure that funds are used properly during lending and borrowing.
