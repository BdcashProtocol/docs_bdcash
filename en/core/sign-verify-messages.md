# Sign / Verify Messages

## signMessage(key, message)

This method is used to sign a message through a private key. It is possible to use this method to prove that you own a certain address or to sign a certain data.

The method will return the signed message, the hash of it, the actual signature, the public key necessary to verify the data and the address that generated the signature.
```
const scrypta = new ScryptaCore

var privkey =  'Sq9GWa9vyM1HghsnVan5UJhtx2GumTaLBTHgDhCW4abjzZLmsYmr'

var message =  'Any cool message to sign and verify!'

let signed =  await scrypta.signMessage(privkey, message)

/*

 {

 "message":"Any cool message to sign and verify!",

 "hash":"b03f58edbc303aae60f1a9fee1bb0640e39062db114f9ba85d85d5475ac49009",

 "signature":"a6587004976105f4fee0cc88aa5afbf8281ff29f2510b04fec66b970a5facd5a06e4c5bc31de10e9ceeb3eae36151cb9b5a2ee10f4d01d2a0959b8148d776abd",

 "pubkey":"027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0",

 "address":"LdRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2"

 }

*/
```
## verifyMessage(pubkey, signature, message)

To verify a message it is necessary to have the message itself, the signature that was placed on it and the public key that generated that signature. If everything is correct, if the message has not been altered and the signature is verified by means of the public key, an object containing the same elements as the previous method will be returned. If something does not match, the method will answer with `false`.

```
const scrypta = new ScryptaCore

var message =  'Any cool message to sign and verify!'

let signature =  'a6587004976105f4fee0cc88aa5afbf8281ff29f2510b04fec66b970a5facd5a06e4c5bc31de10e9ceeb3eae36151cb9b5a2ee10f4d01d2a0959b8148d776abd'

let pubkey =  '027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0'

let verified =  await scrypta.verifyMessage(pubkey, signature, message)

​

/*

 {

 "address":"LdRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2",

 "pubkey":"027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0",

 "signature":"a6587004976105f4fee0cc88aa5afbf8281ff29f2510b04fec66b970a5facd5a06e4c5bc31de10e9ceeb3eae36151cb9b5a2ee10f4d01d2a0959b8148d776abd","hash":"b03f58edbc303aae60f1a9fee1bb0640e39062db114f9ba85d85d5475ac49009",

 "message":"Any cool message to sign and verify!"

 }

*/
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2ODYzMTgzNzldfQ==
-->