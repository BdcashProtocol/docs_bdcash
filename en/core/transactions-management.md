# Transactions Management

## listUnspent(address)

It allows to obtain the list of "unspent" (UTXO) of a specific address. The answer contains an array of UTXO that will be used to build transactions.

Usually this method is invoked internally but can be used to check the balance of the address, for example.
```
const scrypta = new ScryptaCore

let address =  'LLLjx7yV4nhUzSapBAHogb5BdgUR6VCB3o'

let unspent =  await scrypta.listUnspent(address)

/*

 [{

	 address: "LLLjx7yV4nhUzSapBAHogb5BdgUR6VCB3o",

	 amount: 0.05,

	 block: 425041,

	 scriptPubKey: "76a9140c40c2919e3f84e43d7b1c6e808d4690480202ac88ac",

	 txid: "202d34a32e0deaa897bddac60109b844f3be72d2511d56057dd15470f04b6252",

	 vout: 1,

	 _id: "5da6cbb2419ec86f07938358"

 }]

*/
```

## sendRawTransaction(rawtransaction)

It allows you to send a "raw transaction" to the Scrypta network. This method accepts as input the hexadecimal representation of the transaction you want to carry out, already signed by the private key of the address. Generally this method is invoked internally. The answer is a TXID (if the raw transaction is valid, `null` if it is invalid).
```
const scrypta = new ScryptaCore

let rawtransaction =  "0100000002c94e2f1b0d71f956c9b9798119c3db3b610deca3951130c090b17ff9946faeb4000000006a473044022026a088d7054742fe490475286b1e9a2f3e29b3e3c02e813715e8d63001bb66ae0220597b57f2c3655b50c356a81448de3e3a3d495acc1094b04006c0307ec2144e7a0121027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0ffffffff6868a7f754e6254b606d5aa5dcebb27ad9810ddf43ace7338f2a52e5280b07cb000000006a473044022015e0a3b5afd19b8b5bf4d22fa5ed2497b684feed45c2fdce6e6c265e547e9ebb02201010ce6bfbcdec45652a7eca48a588fc5e0870bd1d9e029139d5d147aec2e1a40121027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0ffffffff0200e1f505000000001976a914c79cff4d91a84d05cd2ac5a2fea4e87579f7474088ac2018e505000000001976a914c79cff4d91a84d05cd2ac5a2fea4e87579f7474088ac00000000"

let txid =  await scrypta.sendRawTransaction(rawtransaction)


/*

 Answer:

 823fcfb6c5701153aa5ec0e8d68416a22433fe4237662fb8e0ca2ed41608dc7f

*/
```

## decodeRawTransaction(rawtransaction)

It allows you to decode a raw transaction to reconstruct its original content, i.e. the inputs used and the outputs of the transaction.
```
const scrypta = new ScryptaCore

let rawtransaction =  "0100000002c94e2f1b0d71f956c9b9798119c3db3b610deca3951130c090b17ff9946faeb4000000006a473044022026a088d7054742fe490475286b1e9a2f3e29b3e3c02e813715e8d63001bb66ae0220597b57f2c3655b50c356a81448de3e3a3d495acc1094b04006c0307ec2144e7a0121027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0ffffffff6868a7f754e6254b606d5aa5dcebb27ad9810ddf43ace7338f2a52e5280b07cb000000006a473044022015e0a3b5afd19b8b5bf4d22fa5ed2497b684feed45c2fdce6e6c265e547e9ebb02201010ce6bfbcdec45652a7eca48a588fc5e0870bd1d9e029139d5d147aec2e1a40121027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0ffffffff0200e1f505000000001976a914c79cff4d91a84d05cd2ac5a2fea4e87579f7474088ac2018e505000000001976a914c79cff4d91a84d05cd2ac5a2fea4e87579f7474088ac00000000"

let txid =  await scrypta.decodeRawTransaction(rawtransaction)

​

/*

 Answer:

 {

 "transaction":

 {

 "txid":"823fcfb6c5701153aa5ec0e8d68416a22433fe4237662fb8e0ca2ed41608dc7f",

 "version":1,

 "locktime":0,

 "vin":

 [

 {

 "txid":"b4ae6f94f97fb190c0301195a3ec0d613bdbc3198179b9c956f9710d1b2f4ec9",

 "vout":0,

 "scriptSig":

 {

 "asm":"3044022026a088d7054742fe490475286b1e9a2f3e29b3e3c02e813715e8d63001bb66ae0220597b57f2c3655b50c356a81448de3e3a3d495acc1094b04006c0307ec2144e7a01 027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0",

 "hex":"473044022026a088d7054742fe490475286b1e9a2f3e29b3e3c02e813715e8d63001bb66ae0220597b57f2c3655b50c356a81448de3e3a3d495acc1094b04006c0307ec2144e7a0121027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0"

 },

 "sequence":4294967295

 },

 {

 "txid":"cb070b28e5522a8f33e7ac43df0d81d97ab2ebdca55a6d604b25e654f7a76868",

 "vout":0,

 "scriptSig":

 {

 "asm":"3044022015e0a3b5afd19b8b5bf4d22fa5ed2497b684feed45c2fdce6e6c265e547e9ebb02201010ce6bfbcdec45652a7eca48a588fc5e0870bd1d9e029139d5d147aec2e1a401 027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0",

 "hex":"473044022015e0a3b5afd19b8b5bf4d22fa5ed2497b684feed45c2fdce6e6c265e547e9ebb02201010ce6bfbcdec45652a7eca48a588fc5e0870bd1d9e029139d5d147aec2e1a40121027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0"

 },

 "sequence":4294967295

 }

 ],

 "vout":

 [

 {

 "value":1,

 "n":0,

 "scriptPubKey":

 {

 "asm":"OP_DUP OP_HASH160 c79cff4d91a84d05cd2ac5a2fea4e87579f74740 OP_EQUALVERIFY OP_CHECKSIG",

 "hex":"76a914c79cff4d91a84d05cd2ac5a2fea4e87579f7474088ac",

 "reqSigs":1,

 "type":"pubkeyhash",

 "addresses":["LdRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2"]

 }

 },

 {

 "value":0.989,

 "n":1,

 "scriptPubKey":

 {

 "asm":"OP_DUP OP_HASH160 c79cff4d91a84d05cd2ac5a2fea4e87579f74740 OP_EQUALVERIFY OP_CHECKSIG",

 "hex":"76a914c79cff4d91a84d05cd2ac5a2fea4e87579f7474088ac",

 "reqSigs":1,

 "type":"pubkeyhash",

 "addresses":["LdRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2"]

 }

 }

 ]

 },

 "status":200

 }

*/
```
## build(password, send = false, to, amount, metadata = '', fees = 0.001, key)

This is the main method for building transactions. It internally invokes all the methods listed above.

It is usually invoked internally by the `send` and` write` methods but can be used to build a raw transaction. The output varies according to the `send` parameter.

1.  **Send = false**:the output consists of an object containing the inputs used and the signed raw transaction to be sent later with the `sendRawTransaction` method
    
2.  **Send = true**:  the output is composed only of the TXID
    

The parameters are described below:

-   **key:** the identity payload to use.

-   **password:** the password to de-encrypt the identity payload.
    
-   **send:** it allows to send the transaction contextually (default is `false`).
    
-   **to:** the receiving address.
    
-   **amount:** the amount of Lyra to be sent.
    
-   **metadata:** text string to be written in transaction (maximum 8000 bytes), it is not mandatory.
    
-   **fees:** the amount of fees to use for the transaction, by default they are **0.001 LYRA.**
    

## send(password, to, amount, metadata = '', key = '')

Allows you to send funds to a Lyra address. The method invokes the previous `build` to create the transaction, and the` sendRawTransaction` method to send it. The input parameters are the same as the previous ones, the only difference is that the `key` parameter becomes optional. If not specified, the payload inside the localStorage is used.
```
const scrypta = new ScryptaCore

let address =  'LdRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2'

let password =  'AStrongPassword'

let amount =  1

let metadata =  ''

let txid = scrypta.send(password, address, amount, metadata)​

/*

 Answer:

 823fcfb6c5701153aa5ec0e8d68416a22433fe4237662fb8e0ca2ed41608dc7f

*/
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU0NjA2NTA4NiwzNjA0MTA2MjJdfQ==
-->