# ScryptaID Login Module

## Description
*ScryptaID Login Module* is the tool to implement the login with ScryptaID within any site!

- Interaction with Manent App, the login credentials pass from the mobile device to the dApp in a few seconds.
- Possibility to request one or more mandatory identifiers: only blockchain identities against the website, verified by, for example, e-mail or telephone, have access to the website.
- Ability to force the Gateway: build your own identity Gateway.

> The ScryptaID Login Module code is verified (and verifiable) in blockchain thanks to the blockchain versioning tool.


Recall that ScryptaID Login Module is an open-source software, the repository can be inspected at the [following link](https://github.com/scryptachain/scrypta-login).

### Test
Here is a simple test page to test the functioning of the module:
[https://scryptachain.github.io/scrypta-login/](https://scryptachain.github.io/scrypta-login/)

## Main Features

This tool is useful if you need to easily implement a login system with Scrypta. By default the tool produces an UI where the user can enter with:

- Manent App: by usign the remote signing tool
- Sid File: manually import previoysly stored .sid file
- QR card: using a printed card

You can even choose what kind of identities the user must have so you can recognize him as a qualified user or leave the required attribute blank to allow anonymous users.

## How to use it

First of all you need to include it in your project by including the `scrypta.login.min.js` file like:

```
<script src="./scrypta.login.min.js"></script>
```

You can even use the IPFS version, the hash is: `Qmf8VEsWNnYP9KSV4FybEKPqxeiAG6eWyWo63USfmqkybY` like this:

```
<script src="https://ipfs.io/ipfs/Qmf8VEsWNnYP9KSV4FybEKPqxeiAG6eWyWo63USfmqkybY"></script>
```

Then you need to write the rendering html, where you want to render the button:

```
<div id="scrypta-login" dapp="Demo dApp" callback="testCallback" required="phone"></div>
```

You can customize the login process by including these attributes:
- _dapp_: customize showed title
- _callback_: call the given callback when the login is successful, is **required** if you include one or more required identities, the return object will include it
- _required_: the list of required identifiers separated by a comma (ex. phone,mail,ethereum,twitter)
- _gateway_: if you want to admit one or more identity gateways, in this case you need to insert one or more pubkeys (ex. `0240f294ef20c7bbb82bae24d8d22c7ab94d195adf153162482b6bf540393d7dd5`)

## Test the project

If you want to test it you can simply download the package with `git clone`, install all dependencies with `npm install` and run the development enviorment with `npm run dev`.

## Check the integrity with the blockchain

If you need to check the integrity of the file please use `scrypta-bvc` tool as documented here: [https://github.com/scryptachain/scrypta-blockchain-versioning-cli](https://github.com/scryptachain/scrypta-blockchain-versioning-cli).

All the updates will be uploaded at [https://proof.scryptachain.org/#/address/LiRXTmP4fe8Q3C3c9VtzzPHaxhMWnVRpTh](https://proof.scryptachain.org/#/address/LiRXTmP4fe8Q3C3c9VtzzPHaxhMWnVRpTh)

## Demo page

Check out this link to run a simple demo, available even at `webpack/dist/index.html`: 
[https://scryptachain.github.io/scrypta-login/](https://scryptachain.github.io/scrypta-login/)
