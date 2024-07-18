# Module 4 Unit 4 Create and Transfer Native Assets

## Bob creates a Native Asset using the CLI

*Reminder: these instructions assume you have a running and synced Cardano node - accessible through the cardano-cli tool.* 

### Create Minting Keys
Policies are the defining factor under which tokens are minted. Only those in possession of the policy keys can mint or burn tokens under a specific policy. In this simple case, Bob is the owner, but this could be a group using multi-sig.

Bob creates a key pair like before:

```cmd
cardano-cli address key-gen \
		--verification-key-file asset_policy.vkey \
		--signing-key-file asset_policy.skey 
```
  	 
### Hash the Key
Bob hashes the key he just generated. He will use this later to to create the policy script:

```cmd
POLICY_HASH=$(cardano-cli address key-hash \
		--payment-verification-key-file asset_policy.vkey \
		--signing-key-file asset_policy.skey) 


echo “My policy hash is $POLICY_HASH”
My policy hash is 540b538069c30875...404a265933a3fab4c41
```

### Create a Policy Script
Bob now creates a file that defines the policy verification key as a witness to sign the minting transaction. Bob doesn’t bother with further conditions such as token locking or requiring specific signatures to successfully submit a transaction with this minting policy. Many NFT sales will have a time-lock to create artificial scarcity. More complex sample policy scripts are available on GitHub. Bob creates a new policy.script with the following json content, replacing the required values with the data gathered in the previous steps:

```cmd
{
    "keyHash": "540b538069c30875...404a265933a3fab4c41",
    "type": "sig"
}
```

Remember to replace the <POLICY_HASH> string with the value you generated.

```cmd
echo "{\"type\": \"sig\", \"keyHash\" : \"$POLICY_HASH\" }" > policy.script 

jq ‘.’ policy.script

{
  "type": "sig",
  "keyHash": "540b538069c30875...404a265933a3fab4c41"
}
```

### Compute the Policy Id
To mint the native assets, Bob now needs to generate the policy ID from the script file he just created.

```cmd
$POLICY_ID=$(cardano-cli transaction policyid --script-file policy.script) 

echo "My policy id is $POLICY_ID"

My policy id is eea157d949cf2d30f1648…40a2392629ef8f059
```

Bob saves the output in the POLICY_ID variable as he will need it later.

### Define the Token to Mint
Bob now needs to define the name of his token and the amount that he wants to mint. Since token names need to be base16 encoded, he uses the ‘xxd’ command to encode the token name. The xxd command allows you to create a hex dump from a file.

```cmd
TOKEN_NAME =$(echo -n "Cardano Summit Pass" | xxd -ps | tr -d '\n')
echo "Token name encoded is $TOKEN_NAME"
```
Token name encoded is 54657374746F6B656E

```cmd
TOKEN_NAME="54657374746F6B656E" 
TOKEN_AMOUNT="10000000" 
```

### Build the Transaction
As we saw in earlier units, building a transaction requires knowledge of the available UTXO in the address. Bob uses the following command to query his address:

```cmd
cardano-cli query utxo --address $bob_staking_addr –-mainnet 


  TxHash                                 TxIx        Amount
-----------------------------------------------------------------
62a8fc5d8870672fdac1fbbdd209553cdf4334153e67287b98678d6ccf6e00df     1        9899668558 lovelace + TxOutDatumNone
```

As before, Bob needs each of these values in his next transaction, so stores them in variables.

```cmd
TX_HASH="insert TxHash here" 
TX_IX="insert TxIx here" 
TX_AMOUNT="9899668558"
```
This is what our transaction looks like:

```cmd
cardano-cli transaction build \ 	
	--tx-in $TX_HASH#$TX_IX \ 
	--tx-out $bob_staking_addr+$TX_AMOUNT+”TOKEN_AMOUNT $POLICY_ID.$TOKEN_NAME \
  	--mint “$TOKEN_AMOUNT $POLICY_ID.$TOKEN_NAME” \
	--minting-script-file policy.script \
	--change-address $bob_staking_addr 
  	–-out-file mint.raw
```

Here's a breakdown of the syntax for the ‘tx-out’ parameter:

Bob needs to specify which address will receive the transaction. In this case, Bob is sending the tokens to his own address initially, ie. $bob_staking_addr

The exact order is as follows, note there are no spaces unless stated:

1. address hash  (in this case, Bob’s staking address from earlier unit)
2. a plus sign
3. the amount in Lovelace (ada) 
4. a plus sign
5. quotation marks
6. the amount of the token
7. a blank/space
8. the policy id
9. a dot
10. the token name 
11. quotation marks  

Bob runs the ‘transaction view’ command to inspect his output file, mint.raw

```cmd
cardano-cli transaction view --tx-body-file mint.raw
```

### Sign the Transaction
Transactions need to be signed by Bob to prove the authenticity and his ownership of the policy key.

```cmd
cardano-cli transaction sign \
	--signing-key-file bob_stake.skey \ 
	--signing-key-file asset_policy.skey \ 
	--mainnet \ 
	--tx-body-file mint.raw \ 
	--out-file mint.signed
```

### Submit the Transaction
Bob is ready to submit the transaction, therefore minting his assets (Cardano Summit Passes):

```cmd
cardano-cli transaction submit \ 
	--tx-file mint.signed \ 
	--mainnet

Transaction successfully submitted.
```
After a couple of seconds, Bob can check the output address to ensure it holds his newly minted assets

```cmd
cardano-cli query utxo --address $bob_staking_addr –-mainnet


TxHash                                 TxIx        Amount
------------------------------------------------------------------
05faf31b9626187861cf8f567c2ac92a8da525b05a8a9e013f56d41b3a65efed     0        9899468558 lovelace + 10000000 eea157d949cf2d30f16484cb1891a123892667540a2392629ef8f059.54657374746f6b656e + TxOutDatumNone
```

## Example - Bob sends a ‘Cardano Summit Pass’ token to Alice
To send tokens (Cardano Summit Passes) to Alice’s wallet, Bob needs to build another transaction - this time only without the minting parameter. He sets up our variables accordingly.

```cmd
$ receiver=$(cat alice_address)
$ receiver_output="10000000"
$ txhash="d82e82776b3588c…..ca9fba4ad11f50803a43190"
$ txix="0"
```

Bob fetches the same variables used previously in the minting process:

```cmd
echo Tokenname: $TOKEN_NAME
echo Policy ID: $policyid
```

Bob wants to send ten of his tokens, Testtoken, to Alice's address. These ten ‘Cardano Summit Passes’ are gifts for members of her Cardano meetup group.

Note: Bob needs to send a minimum of 1 ada (1000000 Lovelace) to Alice’s wallet address. He can not send tokens by themselves. So he needs to factor this value into the output. Bob references the output value of Alice’s address with the variable receiver_output.
Since he will send 10 of his tokens to Alice’s address, he is left with 999990 of 

```cmd
$TOKEN_NAME.

cardano-cli transaction build \ 
	--tx-in $txhash#$txix \
	--tx-out $receiver+$receiver_output+"10 $policyid.$tokenname" \
	--change-address $bob_staking_addr \
	--out-file rec_matx.raw
```

Bob signs, and then submits the transaction:

```cmd
cardano-cli transaction sign \ 
	--signing-key-file bob_stake.skey \
	--mainnet \
	--tx-body-file rec_matx.raw \
	--out-file rec_matx.signed

cardano-cli transaction submit \ 
	--tx-file rec_matx.signed \
	--mainnet
```

After a few seconds, Alice should see the POAP NFT, for her Cardano Summit event attendance, in her light wallet. 

## Example - Bob burns his tokens using cardano-cli
Bob reaches the last phase of the token lifecycle. He wants to burn 5000 of the newly minted tokens $TOKEN_NAME, thereby destroying them permanently. Like before, Bob checks his address:

```cmd
cardano-cli query utxo --address $bob_staking_addr –-mainnet
```

Most of the variables remain the same as before, but he needs to update the following variables: 

```cmd
txhash="insert your txhash here"
txix="insert your TxIx here"
burnoutput="0"
```

Burning tokens is fairly simple. Bob just needs to issue a new minting action, but this time with a negative input. This will subtract the amount of the token. He also needs to specify the amount of tokens left after destroying. The same as we saw before when transferring ada, transactions with native tokens also need to add up so input(s) = output(s). So Bob’s calculations are as follows: 

**amount of input token — amount of destroyed token = amount of output token**

```cmd
   cardano-cli transaction build \ 
	--tx-in $txhash#$txix \
	--tx-out $bob_staking_addr+$burnoutput+"9995000 $policyid.$TOKEN_NAME"  \
	--mint="-5000 $policyid.$TOKEN_NAME" \
	--change-address $bob_staking_addr
	--minting-script-file policy.script \
	--out-file burning.raw
```
Bob signs the transaction:

```cmd
   cardano-cli transaction sign \ 
	--signing-key-file bob_stake.skey  \
	--signing-key-file asset_policy.skey  \
	--mainnet  \
	--tx-body-file burning.raw  \
	--out-file burning.signed
```
…then sends (submits) the transaction:
```
   cardano-cli transaction submit \
	--tx-file burning.signed \
	--mainnet 
```
Bob then checks his address to confirm:

```cmd
cardano-cli query utxo --address $bob_staking_addr –-mainnet
```
Bob now sees 5000 tokens less than before:

```cmd
TxHash 		                      TxIx      Amount
------------------------------------------------------------------
f56e2800b7b5980d…e2571b712cf53fb3     1        989643170 lovelace + 9995000 45fb072eb2d45b8b…3fc8ebe8c1af5194ea9c.54657374746F6B656E
```

## Example - Bob mints an NFT and sends it to Alice
Bob wants to mint a Cardano Summit POAP NFT for Alice. As it is a simple use case, he decides to use the simple CIP-25 standard which will attach an IPFS storage reference to his token.

Most NFT projects make the policyID under which their NFTs were minted publicly available on marketplaces. Anyone browsing the project can spot copycat NFTs. With so many scams and rug pulls in the space, most services offer to register your policyID so they can detect scam tokens that are otherwise hard to decipher. More often than not, the only difference to the naked eye can be the policyID.

### Metadata 
In addition to the unique policyID Bob can also attach metadata to a transaction. Metadata is typically formatted in json as follows:

```json
{
   "721": {
       "{policy_id}": {
           "{policy_name}": {
               "name": "<required>",
               "image": "<required>",
               "mediaType": "<optional>",
               "files": [
                   {
                       "name": "<required>",
                       "src": "<required>",
                       "mediaType": "<optional>"
                   }
               ]
           }
       }
   }
}
```

Bob decides to include the following properties for his POAP NFT:
1. Amount: One, a single NFT
2. One defined signature allowed to mint (or burn) the NFT.
3. The signature expires in 20000 slots, to leave the room if corrections are needed. 
4. IPFS link of uploaded ‘Cardano Summit 2023’ image 

The process for minting NFTs is very similar to before, with a few minor adjustments. 

### Set variables​
Bob sets the variable $realnftname and then converts it to $nftname (hex format):

```cmd
realnftname="Cardano Summit POAP"
nftname =$(echo -n $realnftname | xxd -b -ps -c 80 | tr -d '\n')
tokenamount="1"
fee="0"
output="0"
ipfs_hash="bafybeiglkbeiwxqa52gbocs4vicegtdeoj6yrc63izwcxifs2lsim6kfoa"
```

The IPFS hash is a key requirement and can be found once you upload your image to IPFS. Here's an example of how the IPFS CID (content id) looks like when an image is uploaded in [web3.storage](https://web3.storage/)

### Generate keys and address​
As each NFT is a unique asset, Bob follows best practice and generates new keys and a new payment address:

```cmd
cardano-cli address key-gen \
--verification-key-file nft_payment.vkey \
--signing-key-file nft_payment.skey
```

As he did before, he uses these two keys to generate an address:

```cmd
	cardano-cli address build \
		--payment-verification-key-file nft_payment.vkey \
		--out-file nft_payment.addr \ 
		--mainnet
```
He saves his address hash in a variable called nft_address:
```cmd
nft_address=$(cat nft_payment.addr)
```

### Fund the address​
Submitting transactions always requires a small fee. Sending native assets requires sending at least 1 ada. Bob makes sure the address he is going to use as the input for the minting transaction has sufficient funds. He confirms his new nft_address and sends some ada to it. 
```cmd
cat nft_payment.addr

addr_vzm8e7stya3kzp85…8a3ew2k90n7gs36c5fte8v
```
### Creating the policyID
Just as Bob did when generating native assets, he generates an ‘nft_policy’ key pair and a policy script. 

```cmd
cardano-cli address key-gen \
	--verification-key-file nft_policy.vkey \
	--signing-key-file nft_policy.skey
```
Instead of only defining a single signature like last time, Bob’s script file needs to implement the following characteristics this time:

1. Only one signature allowed
2. No further minting or burning of the asset permitted after 20000 slots have passed since the transaction was made

His policy.script file looks like this:

```json
{
 "type": "all",
 "scripts":
 [
   {
     "type": "before",
     "slot": <insert slot here>
   },
   {
     "type": "sig",
     "keyHash": "insert keyHash here"
   }
 ]
}
```
Bob needs to adjust two values here, the slot number and the keyHash. He uses the ‘echo’ command to populate his policy.script and ‘jq’ to parse the tip:

```cmd
echo "{" >> policy.script
echo "  \"type\": \"all\"," >> policy.script
echo "  \"scripts\":" >> policy.script
echo "  [" >> policy.script
echo "   {" >> policy.script
echo "     \"type\": \"before\"," >> policy.script
echo "     \"slot\": $(expr $(cardano-cli query tip --mainnet| jq .slot?) + 20000)" >> policy.script
echo "   }," >> policy.script
echo "   {" >> policy.script
echo "     \"type\": \"sig\"," >> policy.script
echo "     \"keyHash\": \"$(cardano-cli address key-hash --payment-verification-key-field nft_policy.vkey)\"" >> policy.script
echo "   }" >> policy.script
echo "  ]" >> policy.script
echo "}" >> policy.script
```
To generate the keyHash, Bob uses the following command:
```cmd
cardano-cli address key-hash --payment-verification-key-field nft_policy.vkey
```
The keyHash is defined as a string and so is wrapped in double quotes. To calculate the correct slot, he queries the current slot and adds 20000 to it. Note the slot number is an integer so doesn’t need double quotes. 
```cmd
$(cardano-cli query tip --mainnet| jq .slot?) + 20000)
```
Bob makes a new file called policy.script and pastes the JSON from above:
```cmd
vi policy.script
```
Bob notes the slot number and saves it in a variable. This is the same ‘slot number found inside of the policy.script file:
```cmd
slotnumber="Add actual slot number here"
```cmd
He saves the location of the script file into a variable as well:
```cmd
script="policy.script"
```
The last step is to generate the policyID:
```cmd
cardano-cli transaction policyid --script-file ./policy.script > policyID
```
### Metadata​
Since Bob has his policy and policyID defined, he adjusts his metadata.json as follows:
```json
{
   "721": {
       "please_insert_policyID_here": {
           "Cardano Summit POAP": {
               "description": "This is my POAP NFT confirming I was at the CF Dubai Summit",
               "name": "Cardano Summit POAP",
               "id": 1,
               "image": ""
           }
       }
   }
}
```
The third element in the hierarchy needs to have the same name as the NFT native asset.
To save this file as metadata.json use the following command:

```cmd
echo "{" >> metadata.json
echo "  \"721\": {" >> metadata.json
echo "    \"$(cat policyID)\": {" >> metadata.json
echo "      \"$(echo $realnftname)\": {" >> metadata.json
echo "        \"description\": \"This is my POAP NFT confirming I was at the CF Dubai Summit\"," >> metadata.json
echo "        \"name\": \"Cardano Summit POAP\"," >> metadata.json
echo "        \"id\": \"1\"," >> metadata.json
echo "        \"image\": \"ipfs://$(echo $ipfs_hash)\"" >> metadata.json
echo "      }" >> metadata.json
echo "    }" >> metadata.json
echo "  }" >> metadata.json
echo "}" >> metadata.json
```
### Building the transaction​
Bob queries his NFT payment address and takes note of the different values present.
```cmd
cardano-cli query utxo --address $nft_payment.addr –-mainnet
```
The output looks something like this:
```cmd
TxHash                     			TxIx        Amount
------------------------------------------------------------
b35a4ba9ef3ce218…74d3ffb3e6eed3ca28     0        1000000000 lovelace
```
Since he needs each of the values for his transaction, he stores them in variables:

```cmd
txhash="insert your txhash here"
txix="insert your TxIx here"
policyid=$(cat policyID)
output=2000000
```
Bob sets his output value to 2000000 Lovelace ( 2 ADA). There are no decimal points as we are measuring in Lovelace. Bob builds his transaction with the now familiar ‘transaction build’ command:

```cmd
cardano-cli transaction build /
	--mainnet \
	--babbage-era \   
	--tx-in $txhash#$txix \
	--tx-out $alice_address+$output+"$tokenamount $policyid.$nftname" \ 
	--change-address $nft_address \  
	--mint="$tokenamount $policyid.$nftname" \
	--minting-script-file $script \
	--metadata-json-file metadata.json  \
	--invalid-hereafter $slotnumber \
	--witness-override 2 \
	--out-file matx.raw
```
He signs, then submits the transaction:
```cmd
cardano-cli transaction sign /
	--signing-key-file nft_payment.skey  \
	--signing-key-file nft_policy.skey  \
	--mainnet --tx-body-file matx.raw  \
	--out-file matx.signed

cardano-cli transaction submit /
	--tx-file matx.signed \
	--mainnet
```
If everything works as it should, Bob sees the following confirmation:

**Transaction successfully submitted**

After a couple of seconds, he can check the output address, which is Alice’s light wallet address in this case.
```cmd
cardano-cli query utxo --address $alice_address –-mainnet

TxHash                     		    TxIx        Amount
----------------------------------------------------------------
e86535386…3fdd766fb23e7f1b490a0e8     0        1518558 lovelace + 1 ad79da1596…e.4b6964646f7330373138 + TxOutDatumNone
```
### Alice admires her POAP NFT​
Alice sees her brand spanking new NFT in her light wallet. Alice or Bob can also verify the transaction in their favourite explorer. 

### Burning NFTs
If Bob messed something up, or if the Summit was cancelled, he could always burn the NFT if the slot defined in the policy script hasn’t elapsed yet. 

```cmd
burnoutput="0"
txhash="Insert the UTXO holding the NFT"
txix="Insert your txix"
burnoutput=2000000
```
Bob sets the output value to 2000000 Lovelace which is equivalent to 2 ADA. This amount will cover the minimum UTxO requirement. Bob’s runs the following transaction to burn (negative mint) the POAP NFT he previously minted to Alice’s wallet address:
```cmd
cardano-cli transaction build /
	--mainnet \
	--babbage-era \
	--tx-in $txhash#$txix \
	--tx-out $alice_address+$burnoutput --mint="-1 $policyid.$nftname" \
	--minting-script-file $script \
	--change-address $nft_address \
	--invalid-hereafter $slot \
	--witness-override 2 \
	--out-file burning.raw 
```
As usual, Bob then signs and submits the transaction:
```cmd
cardano-cli transaction sign /
	--signing-key-file nft_payment.skey \
	--signing-key-file nft_policy.skey \
	--mainnet  \
	--tx-body-file burning.raw \
	--out-file burning.signed

cardano-cli transaction submit /
	--tx-file burning.signed \
	--mainnet
```
