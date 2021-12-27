# Address Management
## createAddress(password, saveKey = true)

It creates an address and save the payload (by default) in the localStorage. If `false` is passed to the second parameter, the method does not save the payload in the localStorage.

Attention: the localStorage is not checked! In case of presence of a previous payload this will be overwritten. Check carefully the backup and write phases of the payloads in your dApp.
```
const scrypta = new ScryptaCore

let password =  'AStrongPassword'

let payload =  await scrypta.createAddress(password,  false)

/*

 {

 "pub":"LLLjx7yV4nhUzSapBAHogb5BdgUR6VCB3o",

 "api_secret":"33239857dbe3d37fd35b807578a0132b",

 "key":"03097163386854cde5801aec574948e15b9e24c79da65414d4e5588e7140846165",

 "prv":"SnvpeER7kdeMFGRimBzV5EJfX2ZfxmAQwin1qAHD2kXb8XRF983g",

 "walletstore":"LLLjx7yV4nhUzSapBAHogb5BdgUR6VCB3o:d287884b4af9e3e844da643646cb17e364cffc018f3704dfe5db1e04429b6a26986c0151a1008403209e6087ba3eaf75c79544ea93437053f60eb527dabba4acee76fad8e9821c4ce3e5cc54e04b0baa100476fb6010a9c426f8372bc9a4f67297244737f9631e02655fff1f10d04fce8f22743b623f024144f1efc7bc91cc3604e8a87a8f080cde7ef140c9f2c1b93d6d5fe275293cc33e8adae78a63ce63e84250fa59e75fb016cb2f4b3871ed32e0e182b56ec4f6578065f782e961606b3e"

 }

*/
```

### Identity payload composition

-   **pub:** the public address generated.
    
-   **api_secret:** a "strong" key that can be used as an encryption key for information written in blockchain.
    
-   **key:** the public key of the generated address. This is for the validation of written information and for the creation of Trustlinks.
    
-   **prv:** the private key of the address, used to spend the funds.
    
-   **walletstore:** the encrypted version of the payload, which must be saved by the user (in localStorage and separately)
    

## buildWallet(password, pub, wallet, saveKey)

This method, which is normally invoked internally, is used to build the encrypted version of the wallet. It is what the `createAddress` method calls` walletstore`. It may also be necessary to invoke this method in other contexts. For example, it could be called if you want to change the password of your saved payload.

In this case you should proceed as follows:
```
const scrypta = new ScryptaCore

let oldpassword =  'WeakPassword'

let newpassword =  'AStrongPassword'

let payload =  await scrypta.readKey(oldpassword)

​
if(payload !==  false){

 scrypta.buildWallet(

 newpassword, 

 payload.pub,

 {

 prv: payload.prv,

 api_secret: payload.api_secret,

 key: payload.key

 },

 true  //Salva il wallet nel localStorage

}
```


As you can see, the public address is out of the identity payload and can be saved without compromising security: the public address is for consultation only.

The public key and public address are two separate entities. The public address is obtained by doing a double hash function from the public key. The public key, on the other hand, is obtained directly from the private key and is the one that allows the validation of the information written and signed on the blockchain.

## initAddress(address)

This method initializes the address, which means that an available IdANode sends a minimal amount of LYRA to the initialized address. In the case of IdANode Scrypta the quantity is ** 0.05 LYRA **. The response obtained from the IdANode includes the TXID of the transaction.
```
const scrypta = new ScryptaCore

let address =  'LLLjx7yV4nhUzSapBAHogb5BdgUR6VCB3o'

let init =  await scrypta.initAddress(address)

/*

 Answer:

 {

 airdrop_tx: "202d34a32e0deaa897bddac60109b844f3be72d2511d56057dd15470f04b6252",

 dapp_address: "LLLjx7yV4nhUzSapBAHogb5BdgUR6VCB3o"

 }

*/
```

## importPrivateKey(key, password) 

This method allows you to import any private key into the local wallet. It is useful for importing other addresses and using them later.

## getPublicKey(privateWif)

This method allows you to recreate the public key of the address starting from its private key.
```
const scrypta = new ScryptaCore

let prv =  'SnvpeER7kdeMFGRimBzV5EJfX2ZfxmAQwin1qAHD2kXb8XRF983g'

let key = scrypta.getPublicKey(prv)


/*

 Answer: 

 03097163386854cde5801aec574948e15b9e24c79da65414d4e5588e7140846165

*/
```

## getAddressFromPubKey(pubKey)

This method allows you to recreate an address starting from its public key, useful to verify that the public key is actually corresponding to the address.
```
const scrypta = new ScryptaCore

let key =  '03097163386854cde5801aec574948e15b9e24c79da65414d4e5588e7140846165'

let address =  await scrypta.getAddressFromPubKey(key)


/*

 Answer: 

 LLLjx7yV4nhUzSapBAHogb5BdgUR6VCB3o

*/
```

## fundAddress(privateKey, to, amount)

This method allows you to send a specific amount of funds using a private key, it is a simplified version of `send` method and can be used when working with multiple private keys without having encrypted wallets.

The response will be of type `boolean`.

```
const scrypta = new ScryptaCore

let prv =  'SnvpeER7kdeMFGRimBzV5EJfX2ZfxmAQwin1qAHD2kXb8XRF983g'

let key = scrypta.fundAddress(prv, 'LSJq6a6AMigCiRHGrby4TuHeGirJw2PL5c', 1)

```