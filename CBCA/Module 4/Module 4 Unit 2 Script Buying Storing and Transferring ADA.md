# Unit 2 - Buying, Storing and Transferring ADA

## Learning Objectives
By the end of this unit, the learner should be able to:
- Understand the different options when choosing a Cardano wallet.
- Set up a wallet using a browser extension and the CLI
- Request tAda (test ada) from the faucet
- Buy ada from a centralized exchange (CEX) and send it to another ada wallet

## Introduction
Hello everyone, and welcome back. I am your lecturer, [lecturer name], and many thanks for joining me today! 

## Table of Contents
For the rest of this module, we’re going to apply what we learned so far and get hands-on with wallets and addresses. We will first acquire some test ada (tAda), then transfer some real ada as well as delegate our stake. We will run through the steps of creating a native asset, as well as explore the dApp and DEX ecosystem.



First, let's introduce two typical Cardano users. Alice and Bob are friends who decide to learn about Cardano together. Alice is a technophobe who prefers friendly GUIs while Bob is a techie who has used other blockchains and command line tools before.

There are a number of resources charting the many projects in a busy ecosystem: 
Cardano Developer Portal
Essential Cardano
CardanoCube
AdaPulse

Any tool or service we use in this module is not an endorsement or investment advice. 

## Choosing a Wallet and Getting Started
So let’s dive in. Alice wants to get some ada and to do so she first needs a wallet. A Cardano wallet is used to store your public and private keys. Technically, ada is not stored in a wallet or a device, it is recorded on a public blockchain. However, ada can only be accessed using unique private keys, which grant the owner the power to make transactions. Losing your seed phrase or private key(s) means losing access to your funds. When wallets or exchanges transfer assets, the assets are typically transferred from one address to another and never actually leave the blockchain.



During the bootstrapping phase of Cardano, most users relied on the Daedalus full node wallet as well as the Yoroi light wallet. As the network was in its formative stages, a full node wallet was more appropriate back then for network security and stability. 

Cardano has progressed a lot since those early days. With the proliferation of CNFTs (Cardano NFTs) and the growing dApp ecosystem, the blockchain has grown in size, and sync times for full-node wallets have become much longer. 




Light wallets now supported dApp interactions through browser APIs, so user preference quickly shifted to light wallets. Scaling solutions like Hydra and Mithril have progressed from proposals in research papers to live projects on mainnet. Mithril is a protocol that improves the speed and efficiency of nodes' syncing times. Hydra is the layer-two solution aiming to increase the transaction speed and minimize transaction costs. (Both will be covered in a future course).

CIP-30 (Cardano dApp Wallet Web Bridge) led to a standard approach for dApp integrations. The wallet ecosystem flourished and today there are over a dozen options to choose from. Everyone has their favorites and it’s best to find what works for you. The Essential Cardano Guide to the Ecosystem lists many of the contributors and projects building on Cardano.

As the wallet is effectively the entry point to crypto, most providers are now positioning themselves as ‘one-stop shops’. They offer everything you need for staking, NFT marketplace integrations, lending, etc. Most wallets are now available as a mobile app or browser extension. Some wallets allow you to buy ada directly from their UI via integrations with payment merchants easing the onboarding experience.



###  Choosing a Wallet 
Remember when we previously talked about custodial vs non-custodial wallets, we are referring to ownership of private keys. Custodial means a central entity is holding the keys to your wallet. Non-custodial means only you have access to, and responsibility for, your recovery phrase and private key(s). Which is the most secure wallet? It really depends on your own criteria and assumes you are following best practice. Any of the solutions we will cover next can be compromised if the owner is complacent or sometimes just plain unlucky.



We will start with ‘Hot wallets’ and work our way down to ‘Cold Wallets’ which are generally seen as more secure. 

Light wallets (aka Web Wallets, aka online wallets) are convenient if you want frequent access to your assets. They are ‘light’ and faster because they do not need to contain a full copy of the blockchain and instead rely on external data providers. You generally need to be connected to the internet when installing a program or adding a browser extension. An important consideration is that light wallets typically store private keys on the user’s device and encrypt them with a ‘spending password’.  Anything online and concerning money is inevitably in the cross-hairs of nefarious actors employing malware, keylogging, or other malicious attacks.

So it is a trade-off of convenience versus risk acceptance. Many users hold their main secret keys on a hardware wallet and use a light wallet for daily use, similar to having a bank account for your savings while carrying ‘petty cash’ in your pocket.

Mobile wallets are app-based wallets installed on a smartphone via the iPhone App Store or Android Play Store. Such wallets are convenient to install and use QR codes for day-to-day transactions. It is best practice to encrypt your mobile wallet with a spending password and activate MFA (Multi-Factor Authentication). Your recovery phrase should be backed up in case your device is lost or stolen, for example, on a paper or a steel wallet in another location.

Desktop wallets are downloaded to your laptop or computer. Most people who have held ada in the longer term would have on-boarded to Cardano using Daedalus. Daedalus is a full-node wallet, which downloads the entire blockchain and must sync each time you use it. They are generally secure and reliable as you are not relying on external parties to provide data. 

On the downside, full-node wallets are not as flexible or portable. They take up more space and take longer to fully sync up depending on your local system’s resources. A full node is only as secure as the system it lives in. If your computer is hacked, or accessed by another user, your wallet is compromised. You are liable to lose your ada if you install malware or give access to malicious actors to your system. It is a good practice to always multiply the layers of security when you can. 

A hardware wallet is a physical device that resembles a USB key or a flash drive. Unlike ‘hot’ wallets, hardware wallets have no connection to the internet, so are considered ‘cold’ wallets. The device generates a random number that is used to create a seed phrase, and in turn, the public and private keys. They can work in tandem with light wallets via a Bluetooth or USB connection, without your keys leaving the device. In such a hybrid setup, it is the light wallet that generates the transaction and sends it to the hardware wallet which signs the transaction. The signed transaction is then sent back to the light wallet and broadcasted to the network.

The disadvantage of the hardware wallet is you risk losing the device or physically damaging it. There are some wallets with proprietary code and others with open-source code. There is an element of trust in the manufacturer, who can add additional (unwanted) functionality via firmware upgrades. Manufacturing standards and conditions can change without your consent or prior knowledge. The hardware wallet space is also constantly innovating with wallets such as Ngrave completely air-gapped and relying on QR codes instead of Bluetooth or USB connections.

As the name implies, a paper wallet is a physical paper document with your seed phrase on it. The wallet can be a written or typed record of your seed phrase or a printed QR code. If you use a paper wallet, make it durable with laminated paper and store a copy in multiple ‘safe’ physical locations. Paper wallets are a good choice if you do not use your funds day to day, and are more interested in HODLing long term. If you lose that paper, and you have no backup, say goodbye to your funds. 

Steel wallets are sturdier versions of paper wallets which are less vulnerable to fire and water, and obviously less likely to degrade or suffer physical damage.


###  Advanced Custody Solutions
Most retail users will choose one of the above options, however, there are more complex custody options available for enterprises. These cater to more advanced users and are mentioned here for completeness.

A hardware security module (HSM) is a traditional security solution for managing digital keys and has been used widely in PKI (public key infrastructure) environments and in the financial services and retail banking sectors. These institutions have been faced with custody challenges for decades and are well-placed to advise on enterprise custodial solutions. This is somewhat ironic as many see crypto as a replacement for such institutions.

The HSM provides a safe environment to interact with your private key while facilitating encryption, decryption, hash function computations, signing, and signature verification. These modules typically come in the form of a plug-in card or an external device that connects directly to a computer or server. An HSM is usually used for the full life cycle of the private keys, including true random number generation (TRNG), symmetric and asymmetric key generation, distribution, rotation, storage, destruction, and archiving. 

Multi-signature wallets require multiple signatures to verify ownership and execute transactions. A multi-sig wallet is a protocol, or construct, built on top of several credentials held in different wallets. It is not only restricted to private keys but can also be constructed out of scripts. When setting up a multi-sig wallet, the owner assigns individual credentials to each trusted party. There can be different configurations and thresholds set, such as m of n signatures required for certain transactions. Multi-signature wallets rely heavily on open-source privacy-focused software.

Multi-part computation (MPC) wallets employ cryptographic data from multiple parties, using multiple devices, to perform calculations using their combined data points without revealing any party’s individual input. Unlike a multi-sig wallet, MPC wallets don’t assign multiple private keys but instead split a single private key into several smaller parts using algorithms. These algorithmically distributed keys are later processed to generate the whole private key. An MPC wallet can execute a verified transaction using a digital signature created by this shared private key. MPC wallets are typically based on proprietary software and therefore reliant on third-party support.

MPC and multi-signature wallets attempt to address some of the shortcomings with single-signature wallets. Both require multiple users to verify and sign transactions. In theory, the chance of hackers compromising all parties simultaneously is unlikely. These solutions are more appropriate for enterprise users, where governance and accountability can be a regulatory requirement. For example, Coinbase Custody, Fireblocks, BitGo and Gemini all offer various insurance guarantees as well as SOC 1 and 2 compliance. 


###  Setting up a Wallet
Equipped with all this information, Alice has a look on the Developer Portal Showcase section and chooses a light wallet. The landing page allows her to simply add a browser extension and prompts her to ‘Create’ wallet. Alice is new to crypto and apprehensive about using real money starting off. Her friend Bob advises her to select ‘Cardano Testnet’ at first until she finds her feet.

Note: Cardano has two testnets which are independent networks, completely separate from the Cardano mainnet. Preview is an early-stage public testnet where updates and hard forks will happen first. Epochs are 1 day long. Preprod is a later-stage public testnet that receives updates and hard forks four weeks before mainnet. Epochs are five days long, protocol parameters are usually the same as mainnet.

Alice proceeds with the ‘Create’ wallet option where she is asked to name her wallet and ‘Create a password’. This is commonly referred to as a ‘spending password’ and must be re-entered before certain operations. She is then presented with her ‘seed phrase’ and a severe warning of the importance of writing these words down offline. The next step in the process is to confirm some of these words back before hitting ‘Verify and Unlock’.

Most wallets now offer the HD Wallet option discussed earlier. Although faster and less cluttered, single-address wallets are not advised as there is less privacy.

As Alice chose ‘Testnet’, she must now request some tAda (test ada) from the testnet faucet. The faucet is like a tap that pours tAda into your testnet wallet on request.

This ‘dummy ada’ can be used on the public Testnets mimicking the standard use on mainnet, ie. test transactions, test development platforms, test stake pool delegation, etc.

Alice chooses ‘Preprod Testnet’ and enters the ‘Receive Address’ she copied from her light wallet browser extension. She has a look around her wallet and notices twenty ‘Receiving Addresses’ under the ‘Address’ tab.

Alice calls Bob to ask him to explain what has just happened. Bob explains to Alice that she just created a seed phrase from which is derived the secret master key of her wallet. From that root key, her wallet can derive account keys which are like unique wallets within a wallet. The account key then derives multiple stake keys and multiple payment keys.



To recap from earlier units, remember an address contains two parts, one that controls spending (the payment part) and another part that controls stake delegation (the delegation part).

It is a common misconception that public keys are the ‘receiving addresses’. This is true to some extent in a simple system that only supports payment transactions, where the public key could be substituted for addresses. In practice, addresses hold metadata used in other aspects of the protocol. For example, in the Shelley era, addresses may also contain:

A network discriminant tag which marks addresses as being part of a testnet, or the mainnet.
A stake reference to take part in delegation.

As we explored earlier in Module 2, addresses may also be used to trigger smart contracts where they refer to a script rather than a public key.

Addresses are derived from your public key and your public key is derived from your private key. You can't go back from the public key to the private key, but you can produce the public key from the private key. An address is then made up of header information, the hash of the payment credentials, and the hash of the stake credentials. You cannot calculate the public key from the address, but you can calculate the address from the public key. Addresses can't be reversed to public keys. Public keys can't be reversed to private keys. This is the magic of the one-way hash, and why it is used so much throughout crypto. 



It may be easier to visualize this process as a tree structure. The seed (recovery phrase) and private key are below ground and inaccessible. The branches represent public keys and the leaves are analogous to a wallet's multiple ‘receiving addresses’.



Alice’s light wallet displays account balances, monitors addresses, and stores private keys. Transactions can also be created from a wallet and submitted to nodes on the network. These nodes relay transactions across the network until they are processed into a block by a block producer.



As Alice is using the testnet, the address format is as follows:
Example of Address
Addr_test1qzllpqsy4stfdfcqnfrckkdnvzjlem8y92ttqzye6k42p832sj4qqdjps638a5g7jet29yevwru2a9trapjh7uggul0sjma3t4

Alice notices the 10,000 tAda she requested from the faucet has arrived in her wallet. Bob congratulates her and suggests she send him some tAda as a first transaction once he sets up his wallet using the CLI.


###  Creating a Wallet Using the CLI
Command line interfaces (CLIs) accept typed commands from the user at a terminal prompt; these commands are then run by the computer. The CLI is accessed via a shell program. 
A shell program gives you deeper access to an operating system's components. From here, you can run programs or manage configurations.

The two widely used CLI shells are Powershell on Windows machines and Bash for Linux and macOS. Bash is an acronym of "Bourne-again SHell" which is a pun on Stephen Bourne, author of the Bourne shell.

The CLI allows us to get more granular results than we might get with the GUI and also supports scripting and automation.

So for example, we can auto-set repetitive tedious tasks to run in the background rather than repeating each click or navigating several dialog boxes within the GUI.

The GUI is no doubt more user-friendly, and many users won’t ever need to use the CLI. Don’t worry, we are just introducing the CLI tool here so you are aware of it. It will take a greater focus in future courses.

The CLI can seem daunting at first but we will go through the basic ‘help’ features so you don’t need to memorize any elaborate command sequences. 

For Cardano, we will use the cardano-cli which you get automatically when you install the Cardano node (cardano-node).

The cardano-cli allows you to interact with the blockchain by connecting to a cardano-node running on your machine.

The cardano-node connects to other nodes in the network and syncs the complete blockchain. The Cardano Developer Portal guides you through the step-by-step process on your chosen OS, Windows or Linux. There is also an in-depth ‘Cardano Node & CLI’ course and video series created by the Cardano Node Product Manager, Carlos Lopez de Lara. 

As the Cardano ecosystem matures, more and more tooling is available as showcased in the Developer Portal. Demeter is one such platform that provides you with infrastructure pre-configured and an in-browser CLI. 

The cardano-cli is like a Swiss army knife for developers which enables you to generate keys, build transactions, create certificates, and do anything else you need to do within your wallet. A command follows a set structure. The cli is made up of a hierarchy of commands, subcommands and sub-subcommands.

Each command is organized into ‘sub-menus’ and when you type in a command it returns the different options available from the path you took. 
Parameters follow the command and give specific context with some details often optional. A command line parameter is a placeholder for a value, and an argument is the value that is passed to the placeholder. Commands are usually run with arguments provided by the user to tailor how a command should be executed.

Parameters are passed with a double hyphen, so the syntax is consistent in the format:
cardano-cli subcommand sub-subcommand --parameters




In documentation and guides, you’ll see the ‘\’ newline character used which just jumps to a new line for better readability. If you are stuck, you can always find out more by just running a given command without parameters. For example, at the command prompt, type:

cardano-cli –help

This returns all the available subcommands. You can always check for more details by adding --version or --help at any stage. As Bob will initially be concerned with ‘addresses’ he explores this option further by typing:

cardano-cli address —help


Bob wants to know more about generating keys types the ‘key-gen’ sub-subcommand to explore further:

 cardano-cli address key-gen –help

To review all the options, review the official CLI command reference. To keep matters simple to begin with, Bob will generate a "leaf key". Most wallet GUIs will use a hierarchy of keys as explained earlier. 

###  Generate Keys and Address
Before Bob can exchange test ada (tAda) with Alice, he needs to create a key pair. Key pairs are used throughout Cardano for many tasks. They come in the form of a public key (vkey suffix for verification key) and a private key (skey suffix for secret key). Bob will use these to build, sign and submit transactions to send and receive tAda. Later in the module, we will send real ada and native assets in a similar fashion.

So Bob will use the cardano-cli ‘address’ subcommand to create payment and secret keys as follows:

cardano-cli address key-gen \
		--verification-key-file bob_payment.vkey \
  	  	--signing-key-file bob_payment.skey

Bob now uses the ‘cat’ command, so he can review the files he just created:

$ cat bob_payment.skey 
{
    "type": "PaymentSigningKeyShelley_ed25519",
    "description": "Payment Signing Key",
    "cborHex": "582090c82cc879ad7adb…5e85d615937fe8df0d9d49"
}


$ cat bob_payment.vkey 
{
    "type": "PaymentVerificationKeyShelley_ed25519",
    "description": "Payment Verification Key",
    "cborHex": "582073a57a4177cb65dbf8e…76f2373cdd6053b21c"
}


Bob now uses the verification key to generate, or ‘build’, an address.

cardano-cli address build \
		--payment-verification-key-file bob_payment.vkey \
		--out-file bob_payment.addr \
  	  	--testnet-magic 1


Note Bob uses the argument ‘-- testnet-magic <integer>’ to specify which testnet he wants to use. In this case, it’s 1 for the ‘Pre-production’ testnet and ‘2’ would be for the ‘Preview’ testnet. Bob then uses the ‘cat’ command which spits out the ‘out-file’ to screen. This is where Bob’s newly created address lies.

$ cat bob_payment.addr 
addr_test1vr2x99uwdkgl3d7553mqyttpfd3nurfn7q50cxsku3u4d4g4gnpje

When using the cardano-cli to generate keys, note that they are generated randomly without following any of the hierarchical deterministic (HD) wallet derivation standards. This is like a single payment address wallet option, as opposed to the HD Wallet option Alice chose earlier. Note that, as is often the case in Cardano, there is more than one way to do this. You can also derive addresses from a recovery phrase using the cardano-address command. 
 
It’s best practice with the CLI to use variables, so we can refer back to them later if we need them in scripts or other commands. So Bob saves his address to a variable ‘BOB_ADDRESS’ then uses the ‘echo’ command to confirm it back to us as follows:

$BOB_ADDRESS=$(cat bob_payment.addr)
echo "Bob's address is: $BOB_ADDRESS"
Bob's address is: addr_test1vr2x99uwdkgl3….7q50cxsku3u4d4g4gnpje

So Bob has just set up an address on the Cardano blockchain, but now he needs to get some funds, but from where or from whom?! He calls his friend Alice and asks her to send him some tAda. He first provides his ‘receiving address’ on the Preprod Testnet,

(addr_test1vr2x99uwdkgl3d7553mqyttpfd3nurfn7q50cxsku3u4d4g4gnpje). 


Alice saves this address as a new contact ‘Bob’ in her friendly wallet GUI and sends him 1,000 tAda. They both verify the transaction in their explorers 

(transaction id : 65388cf645b2ec119b14313f0c58b47a1b74e9f032ef5e84db0c559a171c1528)





Bob runs the following command to query the UTXO in his wallet and gets the confirmation he was looking for in the output:

cardano-cli query utxo \
		--address $BOB_ADDRESS \
  	  	--testnet-magic 1




TxHash  			   			TxIx	   Amount
-------------------------------------------------------
65388cf645b2ec119…84db0c559a171c1528   0	   1000000000

##  Buying ADA from a Centralized Exchange (CEX)
Before buying some ‘real’ ada, Alice creates a new wallet following the same steps as before, except this time she chooses ‘Mainnet’. The GUI and user experience are identical otherwise. The only difference is her ‘receiving address’ format has no test in its prefix on mainnet:


addr1q9qflm25pwc50…jet29yevwru2a9trapjh7uggul0suae7av



To buy their first ada, most users still rely on established Centralised Exchanges (CEX) such as Coinbase, Kraken, Binance, etc. These exchange platforms allow users to exchange or trade between specific assets, similar to the way platforms exist in classic industries like stocks, forex, bonds, gold, ETFs, etc. Cardano (ADA) is available on most of the main exchanges. 

Traditional exchanges (stock market) are centralized. With classic asset trading platforms, the user is often ‘stuck’ inside the platform. You can buy, trade, and hold assets but it’s not possible to self custody. 

Cryptocurrency exchanges (CEX), or digital currency exchanges (DCE), operate similarly allowing users to trade cryptocurrencies or digital assets. They are traditionally seen as the ‘on-ramp’ to crypto as they accept credit card payments and bank transfers in exchange for digital currencies or crypto. Most cryptocurrency exchanges are also market makers that typically take the bid–ask spreads as a transaction commission or, as a matching platform, charge fees.



###  Decentralized Exchanges (DEX)
Most crypto OGs live by the maxim coined by Bitcoin advocate Andreas Antonopoulos “Not your Keys, Not your Coins”. Whoever controls the seed phrase and private keys controls your funds. Storing your crypto assets on a centralized exchange is always a risk as you are trusting a third party. When you have custody of the private key to your wallet, it also allows you to seamlessly interact with Dapps or Decentralised Finance (DeFi) platforms such as decentralized exchanges (DEX). We will explore DEXs in more depth later in this module.

###  Choosing a Centralized Exchange (CEX)
Most users acquire cryptocurrency via one of the many exchanges that operate globally. When choosing an exchange it's important to see which exchanges are available in your country or region and verify their reputation, volume, liquidity, and trustworthiness on platforms like Coinmarketcap, Coingecko, or others. Exchanges have to be compliant with your local government regulations. This usually involves compliance with Know Your Customer (KYC) and Anti-Money Laundering laws.

Bob advises Alice to take a look at the ‘Markets’ tab for Cardano on coinmarketcap.com which lists relevant metrics like ‘Confidence’ and ‘Liquidity’.

Note that most exchanges offer a ‘Pro’ trading interface which can be a little intimidating and overkill for simple transactions.

For newcomers, this familiar experience is convenient and it’s easy to get complacent and leave your assets on a CEX. It’s important to remember that many cryptocurrency exchanges are not insured (like most Western banks are). If they are hacked, your funds which are stored there are at risk of being stolen or lost forever. Since the exchange “holds the keys”, they are prized trophies for hackers to capture. 

Choosing an exchange from the list, Alice creates an account confirming her country of residence and personal information such as:

full name
address
email address and phone number
payment method (to fund your account, most exchanges accept credit cards or bank transfers)
a document ID (passport, driver’s license, ID, etc)

Following Bob’s advice, Alice sets up 2FA verification for enhanced security and funds safety. Most exchanges will require 2-step verification for requests such as password changes, or withdrawal requests. 

Centralized exchanges (CEX) behave like a bank for cryptocurrencies. They handle the decentralized side of the transaction while maintaining an order book. So, if a transaction occurs, you are not usually transacting on the blockchain, rather you are just transacting on a CEX, which is just maintaining records for those transactions on their side.



Let’s zoom out for a moment, and review the typical inner workings of a CEX:


Customer Deposits: Using a payment gateway API, the user deposits fiat currency into the exchange’s wallet. This fiat money is then transferred to the CEX’s wallet, often in return for a transaction fee. Some bank transfers incur no fee. An entry of this user deposit is made in the CEX’s database. 
Buying/selling crypto: The customer can buy, or sell, any crypto supported by the exchange. At this stage, no transaction typically occurs on the blockchain. The CEX uses its trading engine to match buyers with sellers and then updates its database accordingly. The exchange profits by charging transaction fees.
For standard ‘retail investors’, none of their CEX trading history is recorded on the blockchain. The balance you see in your CEX wallet is just a database entry for what the CEX owes you. Most of the centralized exchanges do not share the private keys of user wallets. They don’t need to, as they’re more likely to host specific exchange wallets for each cryptocurrency. 
Customer withdrawals: when a customer wants to withdraw their assets to their own personal crypto wallet, the transfer is generally from the CEX's crypto wallet to the customer’s crypto wallet ‘receive address’, which in turn, is derived from the wallet’s private key.



Note that while this is the typical experience for most ‘retail investors’, CEXs also offer a suite of institutional products and services to help financial services companies and hedge funds safeguard crypto assets. Some of these services offer various custodial solutions featuring features built around multi-sig and Multi-party computation (MPC).

###  Alice is Now Ready to ‘Buy Crypto’
She signs in to her exchange account, verifying her access code via her MFA device.
She selects a Buy/Sell option.
She clicks Buy, enters ADA (Cardano) as the cryptocurrency to purchase. 
She enters the amount of ada she wants to purchase and selects a payment method from the list (usually bank transfers incur less fees than credit or debit card deposit). 

Some exchanges employ ‘cool down’ periods where you may not be able to withdraw for 24-72 hours after the first transaction on a new debit card. 

Alice confirms her purchase via email and enters the 2FA code from her device. She then receives her ada on her CEX account.
Alice's friend Bob emphasizes the importance of not leaving funds on CEXs and advises her to withdraw to her personal wallet ASAP. She takes his advice, chooses the ‘Withdraw’ option, and pastes her wallet ‘receive address’ and confirms the withdrawal request. Most exchanges offer helpful ‘tool tips’ and won’t allow withdrawals to an invalid address structure. 
Alice checks her wallet and sees her balance updated. She reviews the transaction history in her wallet and also via her favorite explorer. Like with everything in Cardano, there are many different options to choose from when it comes to explorer tools.



Bob creates a ‘receiving address’ on mainnet

Bob runs the same command as before, creating a new out-file which he ‘cats’ out to screen. He specifies the ‘--mainnet’ argument instead of testnet. Like he did previously, Bob assigns the address to a variable.

cardano-cli address build \
		--payment-verification-key-file bob_payment.vkey \
		--out-file bob_mainnet_addr.addr \
  	  	--mainnet

$ cat bob_mainnet_addr.addr 

addr1vx2vgf5luq…..9trhl6u6fy9lf6e770agf4srhw
$bob_mainnet_addr=$(cat bob_mainnet_addr.addr)


Bob shares this ‘receiving address’ with Alice so she can send him some real ada on mainnet. Alice adds this address in her ‘Contacts’ section of her light wallet. This is similar to the process most people are familiar with when creating a new contact on their smartphone. She no longer needs to remember the specific address. She sends Bob some real ada and they both confirm the transaction in their favored explorer.


##  Transactions
It’s important to understand that almost everything happens in Cardano as a result of a transaction. A transaction is usually one of the following on-chain events:

Transfer of ada
Transfer of Native Assets
Minting or burning of Native Assets
Posting of delegation certificates on-chain
Stakepool registrations 
Metadata stored on-chain
A governance upgrade proposals
A combination of the above

For now let's keep it simple, Bob wants to send some ada to Alice’s ‘receiving address’ which she shared with him after she set up her light wallet. As Bob is using the cli, he saves Alice's address in a variable.

Echo 'addr1q9qflm25pwc500tzv….2a9trapjh7uggul0suae7av' > alice_address.addr


$alice_address=$(cat alice_address.addr)
###  Build the Tx Payload
Transactions in Cardano are deterministic, meaning they’re predictable ahead of time. This is not the same experience on other blockchains where the same transaction can have different outcomes and transaction fees depending on when it is executed. As we will see, when Bob builds a transaction (Tx), he will provide all the details upfront and know what transaction fees are before he has to proceed. 


Remember from before, we said a UTxO consists of the reference to the transaction that created it (TxId), and its index (TxIx) on the host transaction. A UTxO is associated with an asset value, an address that dictates its spending conditions and other metadata. A transaction can take multiple inputs (consuming multiple UTxOs) and produce multiple outputs (new UTxOs to be used by future transactions).  

Bob first needs to gather the data he needs for the transaction inputs. He needs to identify the transaction hash and index from where he will send funds. Transaction indexes are not shown in most explorers though the order in which outputs are shown usually follows the real order as found on-chain. Yet to fetch the required details, Bob queries all the UTxO locked by  his own address by running the following command:

cardano-cli query utxo \
		--address $bob_mainnet_addr \
  	  	--mainnet

TxHash -----------------------TxIx---Amount—--------- fed2616805689e…4c2289204f87   1      55834279 lovelace + TxOutDatumNone

Bob needs each of these values for his transaction, so stores them accordingly in variables as follows:

bob_TX_HASH="fed2616805689edaf1……c4c2289204f87"
bob_TX_IX="1"
TRANSFER_AMOUNT="50000000"


Bob wants to send 50 ada, so enters 50000000 lovelace, taking into account the transaction fees.

Now he is ready to build the first transaction to calculate his fee and save it in a file called bobtx.raw. He will reference the variables in the transaction to improve readability because he previously saved almost all of the required arguments in variables. 

There are two commands you can use to ‘build’ a transaction. First, there is cardano-cli transaction build-raw  which is used in many guides. Building the transaction using this option means calculating the fees manually, adjusting the outputs and re-running the command. This can be useful to understand how the command functions, however, you will need to use multiple variables and there is more margin for typos and errors.

There is another more convenient command cardano-cli transaction build which calculates the fees for you and automatically returns the change to your wallet. Bob checks what is the expected syntax by typing the command first cardano-cli transaction build.

He notes it is expecting the format --tx-in $txhash#$txix. This is the input UTXO you want to spend. You can spend multiple UTXOs by adding more --tx-in line(s). The --tx-out parameter is the address of the recipient of the output, just ada in this case. The command structure is as follows:

cardano-cli transaction build --babbage era \
		--tx-in $bob_TX_HASH#$bob_TX_IX \
		--tx-out $alice_address+$TRANSFER_AMOUNT \
		--change-address $bob_mainnet_addr \
		--out-file bobtx.raw

Estimated transaction fee: Lovelace 163421

You may be wondering what the change-address parameter is. Remember, we talked previously about UTXOs and that they could only be spent as one whole UTXO. 


This is like if Alice was buying an apple in the shop from Bob with a $5 note. If the apple is $1, she would get $4 back as change. In this analogy, think of the physical notes as UTXOs. If Alice had a UTXO of 5 ada in her light wallet, and wanted to send 1 ada to Bob for his apple, the light wallet automatically creates a transaction with 1 input (the 5 ada UTXO), and two outputs (1 ada UTXO to Bob’s wallet, and 4 ada UTXO sent back as ‘change’ to her light wallet). Light wallet software makes such change management under the covers so Alice doesn’t need to worry about it, auto-generating a change address for her light wallet and sending her change there as one of the transaction outputs.

In this scenario, Bob is sending funds from his CLI wallet, so he has to build the transaction manually and specify his change-address with this parameter. Unless the UTxOs used as input for the transaction cover exactly the outputs and its fees, the outputs include a change address of the wallet that created the transaction. Light wallets generally default the change address to your wallet address, but you can explicitly designate an address using the cli.

Note that if the change is smaller than 1 ADA, this will all be consumed as "fee". For example, if Bob has a single UTXO of 3 ada and is sending 2.5 ada to Alice, the remaining 0.5 ada can not be sent back to the change_address (since it would be in violation of the min-utxo, currently 1 ada) and will be consumed as fee. This is where the process of ‘Coin selection’ is important. CIP-2 is dedicated to the topic, which outlines the different algorithms for choosing unspent coins from a wallet in order to pay money to one or more recipients.

Bob can inspect the transaction to ensure that it is what he is expecting:

cardano-cli transaction view --tx-file bobtx.raw

###  Sign the Transaction
Bob needs to sign the transactions to prove the authenticity and ownership of the payment key (funds). He signs with the private (secret .skey) key he created earlier.

cardano-cli transaction sign \
		--signing-key-file bob_payment.skey \
		--mainnet \
		--tx-body-file bobtx.raw \
		--out-file transfer.signed


The data returned using the ‘cat’ command can be a little messy, so Bob opts to make it neater using jq command along with the ‘.’ filter:

jq ‘.’ transfer.signed

{
  "type": "Witnessed Tx BabbageEra",
  "description": "Ledger Cddl Format",
  "cborHex":"84a30081825868...8d45ef0c89d02950f7970ef5f6"
}



###  Submit the Transaction
Now Bob is finally ready to submit the transaction by running the following command:

cardano-cli transaction submit \
		--tx-file transfer.signed \
		--mainnet 
Bob has now successfully transferred ada to Alice’s light wallet. After a few seconds, he checks the output address:

cardano-cli query utxo \
		--address $alice_address \
		--mainnet \

TxHash-------------------------TxIx---Amount------------------
62a8fc5d88706433…d6ccf6e00df     0      50000000 lovelace + TxOutDatumNone


Alice's balance in her light wallet has now been topped up by 50 ada. She can also verify this in an explorer. As Alice is not a techie, she asks Bob for some advice on which explorer to use going forward. Bob suggests the visually appealing eUTxO.org explorer as it is more intuitive for beginners trying to understand the benefits of eUTXO. Bob favors the new explorer from the Cardano Foundation which has some features around staking, a topic he is keen to explore now he has his wallet set up.

## Review
And with that, we have made it to the end of another unit! To review, we looked at the different wallet options and the rationale for choosing one over another. We went through the steps involved in setting up a wallet as a browser extension, as well as with the cardano-cli. We went through the process of buying ADA on an exchange and withdrawing it to our wallet. We sent some tAda on the testnet from both the browser extension and the cli. We are now set up to continue our journey in the next unit where we’ll explore staking.

## References
[Ref.4.1.1] CIP-30, Cardano dApp Wallet Web Bridge, Cardano.org, Available from:  CIP-30, Cardano dApp Wallet Web Bridge , Accessed: 16 Aug 2023
[Ref.4.1.2] Essential Cardano Guide to the Ecosystem, Available from: https://landing.essentialcardano.io/guide-to-the-ecosystem , Accessed: 16 Aug 2023
[Ref.4.1.3] Testnets faucet, Cardano.org, Available from: https://docs.cardano.org/cardano-testnet/tools/faucet/, Accessed: 16 Aug 2023
[Ref.4.1.4] Cardano Developer Portal, Cardano.org, Available from: https://developers.cardano.org/ , Accessed: 16 Aug 2023
[Ref.4.1.5] Cardano Node Course, IOG, Available from: https://cardano-course.gitbook.io/cardano-course/ , Accessed: 16 Aug 2023
[Ref.4.1.6] Cardano Node CLI Reference, IOG, Available from: https://github.com/input-output-hk/cardano-node-wiki/blob/main/docs/reference/cardano-node-cli-reference.md , Accessed: 16 Aug 2023
[Ref.4.1.7] Cardano Tracking Tools, Cardano.org, Available from: https://docs.cardano.org/new-to-cardano/cardano-tracking-tools/ , Accessed: 16 Aug 2023
[Ref.4.1.8] Cardano Foundation’s Open Beta Phase of New Cardano Explorer, Cardano Foundation, https://cardanofoundation.org/en/news/cardano-foundation%E2%80%99s-open-beta-phase-of-new-cardano-explorer/ , Accessed: 16 Aug 2023
[Ref.4.1.8] CIP 2 - Coin Selection Algorithms for Cardano, Cardano.org, https://cips.cardano.org/cips/cip2/ , Accessed: 16 Aug 2023

## Glossary
Term
Definitions
Light wallet
Light wallets (aka light client, aka light node wallets) have reduced data requirements allowing them to run faster (lighter). Light wallets do not download the blockchain in its entirety, just a fraction of it. They typically work by connecting with a server(s) that allow them to obtain data from the blockchain.
Full node wallet
A full-node wallet does everything that a regular cardano-node does and contains a complete copy of the blockchain ledger. This is why you will notice much greater 'sync times' when opening a Daedalus wallet for example.
Service Organization Control (SOC)
SOC reports enable companies to feel confident that service providers are operating in an ethical and compliant manner. SOC 1 evaluates an organization's internal controls over financial reporting, whereas SOC 2 is an audit that ensures your service providers securely manage your data.
CNFT
NFTs leverage cryptography to make an asset or digital object unique. CNFTs refer to Cardano NFTs specifically.
OG
OG (crypto Original Gangster) is slang for a founder of any early crypto blockchain. A crypto OG can also refer to an early investor in Bitcoin, Ethereum, Cardano, etc.
Shoulder surfing
A shoulder surfing attack is when an attacker can physically view your device screen and keypad to obtain your personal information.


## Questions
Sub-Unit 1


Where are assets stored?  
In public key(s)
On the blockchain ledger (CORRECT ANSWER)
In private key(s)
In wallets

True or False: You can restore all your accounts, private keys, public keys and receiving addresses using just one seed (recovery) phrase.
True (CORRECT ANSWER)
False

Which of the following are ‘full node’ wallets? Select all that apply
Daedalus (CORRECT ANSWER)
MetaMask 
Yoroi
Typhon
Eternl
Flint
GeroWallet

Which of the following are advisable precautions you should take when using a mobile wallet? Select all that apply.
Use a ‘spending password’ (CORRECT ANSWER)
Activate MFA (CORRECT ANSWER)
Only use your device in ‘dark mode’ in the evenings.
Be conscious of shoulder surfing attacks (CORRECT ANSWER)
Backup your seed phrase elsewhere (CORRECT ANSWER)

True or False: A Light wallet contains a full copy of the blockchain.
True 
False (CORRECT ANSWER)
Sub-Unit 2


Where are private cryptographic credentials stored?
AWS
Local bank
Public blockchain
Wallet (CORRECT ANSWER)

Select two options below that require multiple users to verify a transaction.
Mult-sig wallets (CORRECT ANSWER)
Paper wallets
Light wallets
Hardware wallets
Non-custodial wallets
Multi-part computation wallets (CORRECT ANSWER)
Leather wallets
Sub-Unit 3


Select two options below which are the two widely used cli shells.
Windows explorer 
Bash (CORRECT ANSWER)
TextEdit
PowerShell (CORRECT ANSWER)

Which of the following statements are true regarding addresses on Cardano?
Addresses are derived only from your private key 
Your public key is derived from your private key (CORRECT ANSWER)
You can't go back from the public key to the private key, but you can produce the public key from the private key (CORRECT ANSWER) 
You can calculate the public key from the address, but you can’t calculate the address from the public key
Sub-Unit 4


Which of the following is not a Centralized Exchange (CEX)?
Binance
Kraken
Coinbase
Minswap (CORRECT ANSWER)

What is the main risk of storing your crypto assets on a centralized exchange (CEX)? 
It is a Web 2 user experience
You are trusting a third party (CORRECT ANSWER)
You never own the digital asset
It is not trendy to be using centralized services
Sub-Unit 5


True or False: CEXs (Centralized exchanges) usually have more liquidity than DEXs (Decentralized exchanges)
True (CORRECT ANSWER)
False

True or False: Centralized exchanges (CEX) profit by charging transaction fees to users for both FIAT and crypto deposits and withdrawals.
True (CORRECT ANSWER)
False
Sub-Unit 6


When choosing a Centralized Exchange, which of the following are metrics to consider that are often listed on market listing sites?
Liquidity
Price of asset
KYC requirements
All of the above (CORRECT ANSWER)

If Bob wants to receive ada from Alice, what crucial piece of info does he need to share?
Bobs ‘receiving address’ (CORRECT ANSWER)
Alice’s ‘receiving address’
Bob’s private key
Bob’s favorite wallet provider
