## Module 4 Unit 3 Staking

Before Bob can delegate his ada, he must go through a process that involves registering a stake address. This is done by posting a so-called “stake address registration certificate” to the Cardano blockchain. This registration allows Bob to delegate ada and automatically sets up a rewards address where the Cardano blockchain accrues the rewards from such delegation.

Technically such a registration is required because delegation on the Cardano blockchain involves distinguishing between the transaction of ada and the participation of the same ada in the consensus mechanism. This distinction is achieved by modelling it in the address structure and distinguishing between his payment address and stake address. Bob’s ada is always linked to his payment address but can optionally also be associated with his stake address. This allows him to participate in staking, by running his own pool, or delegating his ada to a stake pool.

To mitigate certain economic attacks, a refundable hold (2 ada) is imposed on Bob upon registration, which will be released when his stake address is deregistered. The hold covers the costs of tracking the stake address and maintaining the corresponding rewards account, and it incentivises deregistering unused stake addresses so that the corresponding Cardano blockchain resources can be released.

Picking up where he finished in the last unit, Bob runs the following command to inspect his payment address...

```cmd
$ cat bob_mainnet_addr.addr | cardano-address address inspect
{
    "stake_reference": "none",
    "Spending_key_hash_bech32": "addr_vkh1jnzzd8l…06wk0hnl23mzzmu",
    "address_style": "Shelley",
    "spending_key_hash": "94c4269fe027d1a…bf4349217e9d67de7f5",
    "network_tag": 1,
    "address_type": 6
}
```

The output confirms Bob created an address type ‘6’, but there are eight different types of Shelley addresses as outlined in CIP-19. A type 6 Shelley address can be used to send and receive ada, but whose associated stake can't be delegated.

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/4.3.15.png)

Bob now wants to create a ‘0’ address type as he intends to start staking his ada. A type 0 Shelley address is built from a payment part and a staking key part, so Bob needs to create a new ‘stake’ keypair first. 

```cmd
cardano-cli stake-address key-gen \
		--verification-key-file bob_stake.vkey \
		--signing-key-file bob_stake.skey

$ cat bob_stake.vkey 
{
    "type": "StakeVerificationKeyShelley_ed25519",
    "description": "Stake Verification Key",
    "cborHex": "5820fd9d828ff85294217b77….167114e2c99268906ed58289"
}
```

Bob ‘builds’ a stake type 0 address with his two verification keys: the initial ‘payment’ vkey from the previous unit and his newly created ‘stake’ vkey. 

```cmd
cardano-cli address build \
		--payment-verification-key-file bob_payment.vkey \
		--stake-verification-key-file bob_stake.vkey \
		--out-file bob_staking.addr \
		--mainnet
cat bob_staking.addr | cardano-address address inspect
```

It should look something like this

```cmd
{
    "stake_reference": "by value",
    "stake_key_hash_bech32": "stake_vkh1kevs5lhejnxy3j6…..e6yn8atev5e3jy7asajygx8zx",      
    "stake_key_hash": "b6590a7ef994….b3a24cfd5e594cc644f761d9"
    "spending_key_hash_bech32": "addr_vkh1tc0da5jwszr8f…fcuxxvexggufyvmnhg3r5p2x",
    "address_style": "Shelley",
    "spending_key_hash": "5e1eded24e8086749fd49602….9c70c6664c84712466e774",
    "network_tag": 0,
    "address_type": 0
}
$bob_staking_addr=$(cat bob_staking.addr)
```

This new ‘type 0’ gives Bob the ability to send and receive ada, but also to delegate his ada to a staking pool and receive ada rewards for contributing to the network.
Register stake address 

To confirm some details, Bob checks the protocol parameters...

```cmd
cardano-cli query protocol-parameters \
		--mainnet \
		--out-file protocol_params.json
```

Before Bob can delegate his stake and earn rewards for participating in the protocol, he first needs to register his stake key to the blockchain. Bob inspects the protocol parameters to confirm that this requires a small deposit of 2 ada. The 'grep' command (global regular expression print) is used in searching and matching text files. 

```cmd
cat protocol_params.json | grep stakeAddressDeposit
"stakeAddressDeposit": 2000000,        
```

To register his stake key, Bob first needs to produce a registration certificate. He is not sure about his options so just types in the `cardano-cli stake-address` command first to review the menu options. Bob needs to leverage the `registration-certificate` sub-subcommand in this case: 

```cmd
cardano-cli stake-address registration-certificate  \
	--stake-verification-key-file bob_stake.vkey \
	--out-file registration.cert
```

Bob wants to review the cert, so runs the ‘cat’ (concatenate) command: 

```cmd
cat registration.cert
{
	"type": "CertificateShelley",
	"description": "Stake Address Registration Certificate",
	"cborHex":"82008200581cb6…5f56d6b3a24cfd5e594cc644f761d9"
}
```

Bob is not done yet, he now needs to submit his certificate to the blockchain. For this, he will again use the `address` command. This time he needs to use a few more options to build the transaction. He uses `--certificate-file` flag to include his registration certificate, and the `--witness-override` flag to specify that this will be signed by 2 witnesses: `bob_payment.skey` and `bob_stake.skey`

Bob uses the ‘jq’ command to process the resulting JSON output. ‘jq’ is a powerful linux command for extracting, manipulating, and transforming JSON data. The ‘-r’ flag here is to get raw output with no double quotes.

```cmd
cardano-cli transaction build --babbage-era \
	--mainnet \
	--witness-override 2 \
	--tx-in $(cardano-cli query utxo --address $bob_staking_addr
	--mainnet --out-file /dev/stdout | jq -r 'keys[1]') \
	--change-address $bob_staking_addr \
	--certificate-file registration.cert \
	--out-file tx.raw
```

Next, Bob signs it with both keys then submits it to the blockchain:

```cmd
cardano-cli transaction sign \
	--tx-body-file tx.raw \
	--signing-key-file bob_payment.skey \
	--signing-key-file bob_stake.skey \
	--mainnet \
	--out-file tx.signed


cardano-cli transaction submit \
	--mainnet \
	--tx-file tx.signed
```

## Step 2. Delegation

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/4.3.16.png)


Bob can now delegate from his stake address to a stake pool by posting a so-called ‘delegation certificate’ to the Cardano blockchain. If Bob wants to change his choice of stake pool, he is free to post a new delegation certificate at any time. 

Technically a delegation certificate contains the stake address delegating its stake rights and the stake pool verification key hash to which the stake is delegated. If a stake address is deregistered, the associated delegation certificate is automatically revoked. Newer delegation certificates supersede older delegation certificates.

Bob now wants to delegate his stake. For that, he needs to create a delegation certificate. He inspects the `cardano-cli stake-address` command by just running it as is at the command prompt. To produce the delegation certificate he needs to know the stake pool id of the pool that he wants to delegate to. Bob decides to delegate to the RATS pool run by Charles Hoskinson:

```cmd
cardano-cli transaction submit \
	--mainnet \


cardano-cli stake-address delegation-certificate \
	--stake-verification-key-file bob_stake.vkey \
	--stake-pool-id 5e376d756f6eec4599..5b13cf204a57c703dc251 \
	--out-file delegation.cert
```

Just like before, Bob builds, signs and submits this transaction with the certificate as follows:

```cmd
cardano-cli transaction build --babbage-era \
	--mainnet \
	--witness-override 2 \
	--tx-in $(cardano-cli query utxo --address $bob_staking_addr \
     --mainnet --out-file /dev/stdout | jq -r 'keys[1]') \
	--change-address $bob_staking_addr \
	--certificate-file delegation.cert \
	--out-file tx.raw
cardano-cli transaction sign \
	--tx-body-file tx.raw \
	--signing-key-file bob_payment.skey \
	--signing-key-file bob_stake.skey \
	--mainnet \
	--out-file tx.signed
cardano-cli transaction submit \
	--mainnet \
	--tx-file tx.signed
```


## Step 3. Rewards Distribution

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/4.3.17.png)

Bob’s reward account is used to receive rewards for participating in the Proof of Stake consensus mechanism. For each stake address, there is an associated reward account. The lifecycle of the reward account follows that of the associated stake address. 

## Step 4. Rewards Withdrawal

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/4.3.18.png)

Bob’s rewards in his reward account can be withdrawn to his payment address at any time by using the rewards account balance as an input to a transaction. This transaction follows the Unspent-Transaction-Output (UTXO) architecture, taking the current balance of the reward account as the input amount.

## Step 5. Deregistration

![alt text](https://github.com/cardano-foundation/cardano-academy/blob/main/CBCA/Diagrams/4.3.19.png)

The stake address deregistration certificate contains the stake address that should be deregistered. Registering a stake address creates a corresponding reward account, which is deleted when the stake address is deregistered. The hold (2 ada) paid during registration is then released. It may take 1-2 epochs, but in this time, rewards are still earned.

