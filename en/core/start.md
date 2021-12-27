# Introduction

[**Scrypta Core**](https://github.com/scryptachain/scrypta-core), as anticipated in the introductory chapters, it is the Javascript library that is the basis of the interactions on the client side (therefore user side) and performs, locally - or without consulting external servers - all the functions necessary for managing addresses and transactions.

##  SID File

The Scrypta Core library NEVER saves private keys in the clear and uses them only "on the fly", after the user has unlocked his identity payload. This payload, which we will mention several times, is an encrypted string through the AES-256 protocol and is commonly saved in files with the extension **.sid (Scrypta ID)**.

The password with which the key is encrypted is NEVER saved in the clear. We ask developers to follow these simple rules, which guarantee a first, but essential, security barrier to the unauthorized use of addresses.

The local management of the .sid files takes place by default through the localStorage if used in the browser or, if used with NodeJS, through the files saved in the `db` directory. The library allows by default to use more than one address and, each of these, can be recalled at a later stage or used in dApps through the browser.

## To start

The Scrypta Core library connects the client with one of the available Scrypta IdANodes. However, these nodes can be customized and overwritten during the initialisation phase so as to use a set of personalized IdANodes, recommended especially during the production phase of a dApp.

In this section we will analyze in depth the functioning of each single method inside the library. The library must be inserted into webpacks or other compilers to use it within a web page, or it can be called directly from NodeJS simply by installing it with:

```
npm install --save @scrypta/core
```

Once installed it must be inserted into the javascript script and initialized. Note that it is important to initialize it with the `true` parameter when used in the browser. This setting allows the library to use localStorage instead of the File System.

```
const ScryptaCore = require('@scrypta/core')
let scrypta = new ScryptaCore(true)

let address =  await scrypta.createAddress('AStrongPassword')

/*

 {

 "pub":"LbcJVdgiJoX55HUSDrdPTw58iC465tbEnG",

 "api_secret":"3d25258d0fe27521eb78d2b9a5ff7242",

 "key":"034c6155cb500844ee0e6674a3237a7d3e6be8f0c0080b18cc3f58289724ee5072",

 "prv":"SninxEoZ9qfuPCSsbZm2E8aB61wqpH94nVdDJ7XutoTNMPvzQt8z",

 "walletstore":"LbcJVdgiJoX55HUSDrdPTw58iC465tbEnG:72363f2891a3f7db7b5c9be07cd9a03d727ac0728b80850b3a21e120c9c18fac226c911eff7d95850f01acd3b6b00406abba764aa14bd0d7c75301a8dc4dc0286c6414be3c4d8d16eee9e35faf635ae439070859b4ac29b1d9e12c983b5aa84b8adbd6dbc69dbf731aad802dfe07df1b7dcff793911fb6e027b989ffcc1189fe4646e9a3db211401bb0b1c92a4740779f6178046299c4dacb37e398d0cf93efac018bd7b6c24426787947fefcd6c0bcb9736ab2d1ba4c0b1b87dc6a8720b819c"

 }

*/
```

## Working with the testnet

To work with the Scrypta testnet you need to set the `testnet = true` parameter immediately after initializing it:

```
const ScryptaCore = require('@scrypta/core')
let scrypta = new ScryptaCore(true)
scrypta.testnet = true
```

From now on both addresses and IdANodes will be testnet.

## Library testing and debugging

To test the library locally you must have installed NodeJS and GIT, below the list of commands necessary to start the test web interface:
```
git clone https://github.com/scryptachain/scrypta-core

cd scrypta-core

npm  install

npm run test:local
```
