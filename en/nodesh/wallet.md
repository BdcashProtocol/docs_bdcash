# Wallet

The operations related to the wallet are similar to those of BdcashProtocol  Core or the Qt-Wallet. In general, you can always invoke the wallet's RPC functions, even if not all calls are specified as endpoints.

## Crypto.ts
The module responsible for all interfacing operations is located in `src/libs/Crypto.ts`. This module allows you to call any RPC function through the `request` method. There are several other methods that are called internally and that can be analyzed directly. We describe the `request` method, as it is essential in case you want to extend the functionality of the IdANode.

### request(method, params  = [])

It allows you to send any call to the wallet through the RPC protocol. The list of possible calls is here: [https://docs.bdcashprotocol.com/en/#/wallet/fullnode](https://docs.bdcashprotocol.com/en/#/wallet/fullnode)

It is therefore possible, for example, to call the `getnewaddress` method directly through the `request` method:
```
import  *  as  Crypto  from  '../libs/Crypto'
let  wallet  =  new  Crypto.Wallet
let address = await wallet.request('getnewaddress')
```

**_It is important to note that this method is not reachable from the outside._**

## [POST] /init

This endpoint is used to initialize an address. In strictly blockchain terms, this operation has no particular consequences. An address exists because it is generated (the operation takes place offline) and does not require funds to perform operations related to the signature. However, it may be necessary to "initialize" it, or to make known its existence at a certain moment in time, by sending funds.
The amount of funds sent is decided upstream, within the _.env_ file. In the ScrANTA IdANodes it amounts to **0.05 BDECO**.

The call admits only the **address** field and, if funds are actually sent, it will answer with the relative _txid_. The operation could fail if there are not enough funds in the IdANode to send the transaction.

Here is an example of an answer:
```
{

	"data":  {

		"dapp_address":  "LY6BHLvjNbHCQxnpGgt6BvXhXjfX6Nk1X2",

		"airdrop_tx":  "d963d9d2d4862868ec3a1fa93beca49b4427a5fbb39722face624a06eabe6848"

	},

	"status":  200

}
```

**N.B** this call cannot be made more than once for IdANode as an internal register is kept.

##  [GET] /getnewaddress/:internal

It allows you to generate a new address and returns its private key and public key.

_It is not recommended to use this function if the IdANode is public on the Internet. It would be more correct to generate offline or client-side addresses through the BdcashProtocol  Core library._

The optional **internal** parameter allows you to generate addresses inside the IdANode, i.e. addresses that are saved inside the wallet.dat (the BdcashProtocol  wallet file).

```
{
	"address":"8XVTCseqosHJDD4BzU2Xb1XH6RPJQu7ZUq",
	"private_key":"SpeJ9q3w0DSDqsPYmMr5A1zUtgeFPkhDjHRcttN6PonAGY4JazAK",
	"pub_key":"03b635b83e1473a4b0cd91696926cfa69d1dec030b3e97213f52a45cbc976103a7",
	"status":200
}
```

## [POST] /send
It allows you to send funds directly from the IdANode, specifying the following parameters:
- **from**: the address from which to send the funds
- **to**: the address to send the funds to
- **amount**: the amount you intend to send
- **private_key**: the private key of the address from which you intend to send the funds
- **message**: a possible text message that cannot exceed 7500 Byte and that is inserted as OP_RETURN within the transaction in a secondary output

## [POST] /sendrawtransaction
Allows you to send a previously set and signed raw transaction to the network.

## [POST] /decoderawtransaction
It allows you to decode a raw transaction by converting it from hexadecimal to a JSON object.

## [GET] /wallet/getinfo
Returns the wallet response to the `getinfo` call. Contains synchronization information with the blockchain.

## [GET] /wallet/masternodelist
Returns the response of the wallet to the `masternode list`,` masternode count` and `masternode current` calls thus allowing to analyze the current network.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwODE0Njg4MiwtMTkzMjU2NTYzNCw0MD
A2NDU0OCwtOTUxNTc3NDk1LDIwNTE1NDA2MzksLTU2ODQ4MTAw
LDE5OTU0ODYzNDYsODczMTE0NjE1LC0xMTY5ODM3MjI0LC0xMj
Q1MTU4OTczLDExNzgxNjc5NDIsLTIxODE1MzAxMSwtMjA4ODc0
NjYxMl19
-->