**eUTxO & wallet security** 

The underlying architecture and account model affects how basic tools and services are built. CIP 30 *Cardano DApp Wallet Web Bridge*[^1] led to a standard approach for building wallets on Cardano. There are over a dozen options to choose from on the *Cardano Developer Portal Showcase*[^2] section. Wallets are arguably more secure due to the UTxO model. 

Ethereum wallet drainers often exploit a 'transferFrom' wallet function used to transfer assets from a user’s wallet to a smart contract. Then the 'transfer' and 'approve' functions are manipulated to transfer assets to the attacker's address. Whoever controls the smart contract, controls the funds, as often they can transfer tokens to any external address.  

When users are interacting with a smart contract on Ethereum, they usually have to confirm a 'token approval' transaction to spend a certain amount of tokens from their wallet. This is a completely innocent feature to approve transfers in advance, but it is, nonetheless, vulnerable to attackers. 

**Figure 39**: Common wallet attack on Ethereum 

Once the user signs the 'approve' transaction, the smart contract can run the 'transferFrom' function in future without needing further user approvals. This is a double whammy, as the functions guzzle up gas fees for on-chain transactions and drain a user’s wallet. 

Adversaries typically use tactics like social engineering or phishing to fool users into signing the 'approve' function of a malicious contract. They then abuse the 'transferFrom' function to drain the user’s wallet. It is usually too late by the time a user realizes they’ve unwittingly signed away their assets. 

eUTxO Smart contracts, or validators, don’t have this shoddy approval mechanism. A smart contract can’t grant excessive permissions or access to a wallet. Smart contracts on Cardano are essentially scripts that validate exclusive access to the UTxOs sitting at an address. Cardano nodes on the network run these scripts to validate transactions. 

As Cardano leverages the eUTxO model, assets sit in unspent outputs rather than as account balances. Each UTxO can be consumed only once and in its entirety, so there’s no equivalent 'approve' function to be exploited.  

In summary, the 'approve' function enables a mechanism to allow third parties to periodically withdraw a set amount from your bank account. While it can be a useful function to pay your electricity bill, it requires users to trust the third party not to abuse the permission. The user often forgets the onus is on them to cut off permissions. So a service like *Amazon Prime* can continue to collect a subscription clandestinely, whether you use the service or not. While Cardano’s validators only grant permission if conditions for spending UTxOs are satisfied, Ethereum’s smart contracts can potentially gain too much control over user wallets.

[^1]: CIP-30, cips.cardano.org/cip/CIP-30
[^2]: Cardano Developer Portal, developers.cardano.org/showcase?tags=wallet
