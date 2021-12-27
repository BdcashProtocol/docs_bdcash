# Advanced Wallet Management (Seedphrase - BIP32/39)

## generateMnemonic (language)
Create a 24-word mnemonic phrase (seedphrase), which represents the way to save and recall your wallet.
The possible values for `language` are: `english`, `italian`, `spanish`, `french`, `latin`.

The answer will be like:
```
vespa definire exite foedor quia scando mentio fessus texo fervo malitia ferula lectio mobili praesenti cursoriam initio conditura vocalis calceus fratrem blande invite maligno
```

## buildxSid (password, language, saveKey = false, mnemonic = '', label = '')
This method, which is normally invoked internally, is used to build the encrypted version of the wallet, in xsid format, starting from the mnemonic phrase.

The `mnemonic` parameter can be passed to the method to rebuild a wallet, if left blank the method will create a new wallet.

The answer will be like:
```
 {
  mnemonic: 'supera involucrum quantum nucleus tempus rigidas fimbria linearis porta fontana ignis altum corporis gemitus corporatio mane digno mare ferula canna temere quoque liquescimus motricium',
  seed: '8cdd667aa57d709bf8949a949eeba37cf3719fe564cf02ce7cc5a4e0e14d21471e714132a0d62900f05baa2ce69859e96748bc3ed1b6e696308bf1bde780e3a9',
  xprv: 'xprv9s21ZrQH143K2K3M4nD4kb7qRwSNBYhYSQyHcx6soWm6TXKnxXFY8siipmQXeHPpQ6bt5HC9uUnbuAZiPbNBmzYTRj4bCa3heAwv7HZhPhd',
  xpub: 'xpub661MyMwAqRbcEo7pAok57j4ZyyGrb1RPodttRLWVMrJ5LKewW4Zngg3Cg3i3XaeWBaxp2EYgZA2V1mvY8QtE3hK6Un4pWyPLSFBqCPd89ZM',
  walletstore: 'xpub661MyMwAqRbcEo7pAok57j4ZyyGrb1RPodttRLWVMrJ5LKewW4Zngg3Cg3i3XaeWBaxp2EYgZA2V1mvY8QtE3hK6Un4pWyPLSFBqCPd89ZM:3c76af024e93e793edf6922fa621416f*b3c7e8859ea6aa0e1a9edc79114c83f6a0df7d0c7092af4c022b99b467229dcbc606ef97b5652e777a3b8827900d6cea0eb867afba45d372a02eef50a3407091e41db39365529d95d85b753825d8f393091750af2f2ceaf5454f2458d9e3f4e8d8b2a4fa19c6dfeca3dd835f4fa9a0b6a5acf50c29f12be9063add70a5bc02c675e6b0811a461a2fdf5b09176694cd97079d2ef1ed3ed5144d04b60f190362589ad97fe940b94a0766709db7bc3c0f1c274bd7308ef56dfe'
}
```

Where `walletstore` is the property to save locally, which represents the encrypted form of the xsid.

## returnxKey (xpub)
Return the xsid starting from a given xpub.

## returnXKeysFromSeed (seed)
Returns the derivation keys `xpub` and `xprv`, given a  seed. The seed can be passed either in the form of a buffer or in the form of a hexadecimal.

The answer will be like:
```
{
  xprv: 'xprv9s21ZrQH143K4BiZMkPAfiGhUrZZApVnobQ4TRDNdbqzBbjG3LnSsWCG8qBoZgfCP2ZFdNvqEDvsHYojuzW5wdw1eqR4saxm5iij387tRYg',
  xpub: 'xpub661MyMwAqRbcGfo2TmvB2rDS2tQ3aHDeApKfFoczBwNy4Q4Qat6hRJWjz8mBWbD27z65cfuszxmrcUQxQRepeYJ4tibfW7Q8fjVaLe6bPVf'
}
```

## deriveKeyFromSeed (seed, index) 
This method is used to derive an address starting from a certain seed. The seed must be passed in the form of a hexadecimal and the index must comply with the BIP32 directives.

Here is a complete example:
```
const ScryptaCore = require('@scrypta/core')
const scrypta = new ScryptaCore

scrypta.buildxSid('YourAwesomePassword', 'latin', false).then(async response => {
    let derived = await scrypta.deriveKeyFromSeed(response.seed, 'm/0')
    console.log(derived)
})
```

The answer will be like that and as we can see we will again have the `xpub` and `xprv` derived from the index `m/0` (and which can be used to derive further keys) and we will also find the classic `prv`, `key` and `pub`, which are the keys to be used to perform blockchain transactions.

```
{
  xpub: 'xpub684TvGdzE8Fm4aQoWY3XvnabLXEkrfaceGhonV8cWJYWJB6aqTL6YbtUSQpKrSZ9U2Ks5WSCfeYfDFKkrELSk56p81R2nekwwDFKQ5LePwU',
  xprv: 'xprv9u57Wm76PkhTr6LLQWWXZedrnVQGTCrmH3nCz6izwy1XRNmSHv1qzoZzb7BCP8uBYi6tPVAUfcjawrV2oW8Q3KhMJoAu9dZw1D1QBXf8nLY',
  key: '03846cb51e41b7f5867023b8088461022aef505878a9adea0f1a20af7e06e7bb84',
  prv: 'SmPgNxuKaj2P6HKYbbdjo1PiYpa5UtTb2YYndB9vWWj1wbWWtwK3',
  pub: 'LXzAMht11qUuX3J4p34aLZqXwNrTC9nQTA'
}
```

## deriveKeyFromXPrv (xprv, index)
It derives an address starting from xprv, the use is similar to that previously exposed, as well as the answer.

## deriveKeyFromMnemonic (menmonic, index)
It derives an address starting from the mnemonic phrase, the use is similar to that previously explained, as well as the answer.

## deriveKeyfromXPub (xpub, index)
It derives an address starting from the xpub, the use is similar to that previously explained, the difference lies in the result, as it will not contain the *private keys* but only the public keys.

This method is very useful when used in payment gateways.

The answer will then be like:
```
{
  key: '03a94b4ca4f1c70f5271bcbb34fff862dbd26149bfea442e019b5d72f8a2eebd92',
  pub: 'LdXmmVfZcXjEVCKHKLpnfrZkR12AKRvsmg'
}
```

## hashtopath(hash, hardened = false) 

This method is used to calculate, given a given * hash *, the relative index. It is very useful if used to calculate addresses that always refer to the same information, given a certain seed.

The `hardened` parameter will cause it to return a key that is `hardened` which means that it can derive additional keys, or not.

Here is a concrete example:

```
const ScryptaCore = require('@scrypta/core')
const scrypta = new ScryptaCore

scrypta.buildxSid('YourAwesomePassword', 'latin', false).then(async response => {
    let information = 'MyUniqueAndImportantInformation'
    let hash = await scrypta.hash(information)
    let index = await scrypta.hashtopath(hash)
    let derived = await scrypta.deriveKeyFromSeed(response.seed, index)
    console.log(derived)
})
```
The calculated index will always be: **m/23559354/10589217/16016918/92402432/91797913/43958111/25117371/23712615/23493219/2410221** and the result will be like:
```
{
  xpub: 'xpub6SKuGyKdaSwH8DvhnPVz5se4J2x6BA3AJiFFcvZF4s7g4Re2NttSdSb52E2CiZv9Xc11xKkRyieBURVVEu159ivFbmVf3GVrZ5mQhz76pQR',
  xprv: 'xprvADLYsTnjk5NyujrEgMxyijhKk17bmhKJwVKepY9dWXahBdJsqMaC5eGbAzEcZD5S6R46caiiqipFmiXMvHcDvoS3iYQFfAJwLGtvAw6L846',
  key: '0214bc8fe8d4e3256214da13c32f18d270beded71d99ac0bb9ba8eea116132c5b3',
  prv: 'Sr5bo2kT6KiLKb95aUz37cPLvJGBrGiwFgyzC3qhK4k7Y6uXwrRz',
  pub: 'Lh7ZbcC5CVCnJwRkfut3m8WfSgB4vdAQow'
}
```
