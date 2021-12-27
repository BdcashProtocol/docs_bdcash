# Interaction with Smart Contracts

These methods are used to send calls to Smart Contracts in a simplified form. The search for the node to be queried and the actual call to it are automatically managed.

## createContractRequest(key, password, request)

This method is used to generate a request to a smart contract. Requires you to send:
- *key*: the public key or sid that will make the call
- *password*: the password to unlock the sid
- *request*: the actual request to the contract, in the form of an object, which contains the properties `contract`, `function` and `params`.

Here is an example of how to use it:

```
const ScryptaCore = require('@scrypta/core')
const scrypta = new ScryptaCore
let address = await scrypta.createAddress('MyPassword')
let request = await scrypta.createContractRequest(address.walletstore, 'MyPassword', { contract: "LgSAtP3gPURByanZSM32kfEu9C1uyQ6Kfg", function: "search", params: {contract: "LcD7AGaY74xvVxDg3NkKjfP6QpG8Pmxpnu", version: "latest"} })
```

The response will look like this:

```
{"message":"7b22636f6e7472616374223a224c675341745033675055524279616e5a534d33326b664575394331757951364b6667222c2266756e6374696f6e223a22696e646578222c22706172616d73223a7b22636f6e7472616374223a224c4c734e577179687248327748706838373956585446614e4c4c597434334a6a7136222c2276657273696f6e223a226c6174657374227d7d","hash":"2b8cfaafda8ab93046fcc5e5135472b7c0be2259e8d414eadee99d662cd3934d","signature":"54cb580b23bc0fc63857be8c30f5cb2a37cc016ad64abfeee0a44463f67a84f461f995a287562b6245e80458ce0e97b63b8101511f0f1459ee6fd5bbd5b215f8","pubkey":"0366c39e2700b045c247bce4d8f1a858deae30fac80bf2ce3e1b428dd849f35c01","address":"LXHGeHh83wdMi2sd6tkgnhpPrgWUQSAjTb"}
```

## sendContractRequest(request)

This method sends the request to the first available IdaNode and returns the result. After creating the request, you can send it directly with:

```
let response = await scrypta.sendContractRequest(request)
```

The answer will be present in the variable.