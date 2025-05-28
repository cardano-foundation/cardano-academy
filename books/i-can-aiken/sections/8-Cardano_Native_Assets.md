**Cardano Native Assets**

IOG researchers presented the paper, *UTxOma: UTxO with Multi-Asset Support*,[^1] at the ISoLA 2020 conference. This research explores a novel approach to creating user-defined tokens on a UTxO ledger, using specialized scripts called minting policies. These policies, similar to Bitcoin's validator scripts, employ a domain-specific language with limited computational power, prioritizing security and efficiency. This results in a lightweight and cost-effective method for creating and managing custom tokens. 

The *Native Custom Tokens in the Extended UTxO Model* paper[^2] further develops the eUTxO model to incorporate native user-defined tokens. This research investigates the synergy between these native tokens and expressive smart contracts within the UTxO framework. The result is a system with more flexible minting policies and a direct mapping of state machine-based contracts to the multi-asset eUTxO ledger. The paper also includes a formal proof to establish the correctness of this mapping. 

Cardano implemented this research as a so-called multi-asset ledger in which user-defined custom tokens have all the same functionality and support as the primary currency, ada. In other words, the ledger and the protocol manage tokens without the need for any third parties to supply smart contracts that enforce additional rules–rules which may not be in the best interest of the end user. This design has several advantages for the user. Once the native assets are sent to a user’s wallet, they have **exclusive control over them**. 

Ethereum also allows for various user-defined assets. However, Ethereum’s various token standards are not directly supported at the protocol level. Custom smart contracts are required and re-used, which adds complexity, unpredictable gas fees and general clunky design. This leaves the door open for unintended side effects. On Ethereum, for example, centralized stable coin issuers can freeze or blacklist your account through custom smart contracts.  

This is not possible on Cardano, however, as there is no interference from third-party code. Native assets are transferred more efficiently with minimal transaction fees. As user-defined assets enjoy the same status as ada at the protocol level, they are also very secure. The Cardano protocol has been stress-tested from daily use since 2017 on a blockchain with 100% uptime as of April 2025.

[^1]: UTxOma: UTxO with Multi-Asset Support, iohk.io/en/research/library/papers/utxomautxo-with-multi-asset-support/
[^2]: Native Custom Tokens in the Extended UTxO Model, iohk.io/en/research/library/papers/native-custom-tokens-in-the-extended-utxo-model/
