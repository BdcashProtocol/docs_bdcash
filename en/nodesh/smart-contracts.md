# Smart Contracts

To get a general overview of how Smart Contracts work, read the [initial guide] (/smart-contracts).

Below are the endpoints enabled within the IdaNode to interact with BDCash Smart Contracts.

## [GET] /contracts

This endpoint returns all the contracts published within the BDCash network and the related Javascript codes that can be publicly consulted, as they are executed, updated to the latest version available.

It is important to understand that the code shown is already `compiled`, ie some code is added

## [GET] /contracts/:address

This endpoint returns a single contract, the response will be like:


```
{
    "v": 1,
    "name": "BDCASH NEWS FEED MANAGER",
    "author": "BDCASH TASK FORCE",
    "version": "1.0.0",
    "description": "THIS feed WILL MANAGE ALL THE FEEDS RETURNING A COMPLETE LIST",
    "immutable": "false",
    "code": "const BDCashCore = require('@bdcash-protocol/core'); const db = require('db'); const axios = require('axios');const bdcash = new BDCashCore; bdcash.staticnodes = true;bdcash.mainnetNodeshs = ['http://localhost:3001']; bdcash.testnetNodeshs = ['http://localhost:3001'];/**
	 * NAME: BDCASH NEWS FEED MANAGER
	 * DESCRIPTION: THIS feed WILL MANAGE ALL THE FEEDS RETURNING A COMPLETE LIST
	 * AUTHOR: BDCASH TASK FORCE
	 * VERSION: 1.0.0
	 * IMMUTABLE: false
	 */
	
	// DEFINING COMPILER VERSION
	/* BDCash v0.0.1 */
	
	async function constructor() {

	}
	
	async function eachBlock(block){
		    searchdata(block['data_written'])
	}
	
	async function searchdata(data){
		    if(Object.keys(data).length > 0){
		        let keys = Object.keys(data)
	        for(let k in Object.keys(data)){
		            console.log('ANALYZING DATA FOR ' + keys[k])
	            for(let j in data[keys[k]]){
		                let written = data[keys[k]][j]
	                if(written.protocol === 'rsspin://' && written.data !== 'undefined'){
		                    let check = await db.read({feed: written.data})
	                    if(check.feed === undefined){
		                        let obj = {
		                            feed: written.data,
	                            manager: keys[k],
	                            uuid: written.uuid,
	                            active: true
	                        }
	                        let result = await db.insert(obj)
	                    }else{
		                        await db.update({feed: written.data}, { $set: { active: true } })
	                    }
	                }else if(written.protocol === 'rssunpin://'){
		                    let check = await db.read({feed: written.data})
	                    if(check.feed !== undefined && keys[k] === check.manager){
		                        await db.update({feed: written.data}, { $set: { active: false } })
	                    }
	                }
	            }
	        }
	    }
	}
	
	function index(request) {
		    return new Promise(async response => {
		        if (request !== undefined && request.type !== undefined) {
		            let type
	            if(request.type === 'true' || request.type === true){
		                type = true
	            }else{
		                type = false
	            }
	            let dbo = await db.read({active: type})
	            let feeds = []
	            for(let k in dbo){
		                let feed = dbo[k]
	                if(feed.feed !== 'undefined'){
		                    feeds.push(feed)
	                }
	            }
	            response(feeds)
	        } else {
		            response('Please requests for a feed first')
	        }
	    })
	}
	module.exports.eachBlock = eachBlock;
	module.exports.index = index;
	constructor();",
    "address": "8e9G4AYSGbGqonH7QEjFHDeVAMSPxK9KWt",
    "functions": [
        "eachBlock",
        "index"
    ]
}
```
## [GET] /contracts/:address/:version

This endpoint returns a specific version of a specific contract.

## [POST] /contracts/run

This endpoint initiates a call within the contract and expects a request (in hexadecimal format) signed with the requester's private key.

Using it directly is cumbersome, it is recommended to integrate the relevant call into `@bdcash-protocol/core`.

This request to be sent will be of the type:
```
{
	"message":"7b22636f6e7472616374223a224c675341745033675055524279616e5a534d33326b664575394331757951364b6667222c2266756e6374696f6e223a22696e646578222c22706172616d73223a7b22636f6e7472616374223a224c675341745033675055524279616e5a534d33326b664575394331757951364b6667222c2276657273696f6e223a226c6174657374227d7d",

	"hash":"c20eadaf349bf63ddf8ba437310ce0d2148651f4f2ad8743cb026b2a56b0381e",

	"signature":"eda7d87752ef2b7e1cf3e5e7117306f466f3649d274fc159b4e51f0d433cbf2f1d53640ad2f69aa1bbac2d0b71f6f27489115f2f793d36df447f143f394ba835",

	"pubkey":"022030a7ea2338174bc3350a8f7d59503f7a53b81223c5fc385425562cadb5164b",

	"address":"8SJq6a6AMigCiRHGrby4TuHeGirJw2PL5c"
}
```

To generate it we will use `@bdcash-protocol/core` like so:

```
const BDCashCore = require('@bdcash-protocol/core')
const bdcash = new BDCashCore
let address = await bdcash.createAddress('MyPassword')
let request = await bdcash.createContractRequest(address.walletstore, 'MyPassword', { contract: "8gSAtP3gPURByanZSM32kfEu9C1uyQ6Kfg", function: "search", params: {contract: "8cD7AGaY74xvVxDg3NkKjfP6QpG8Pmxpnu", version: "latest"} })
```

To send it we will use the `sendContractRequest` method like so:
```
let response = await bdcash.sendContractRequest(request)
```

The answer will be like:
```
[
    {
        "pubkey": "03b2131eef9abc87f7f1fd29b3a27c4fb9add53884ece96a4ad7696f86f5e2a168",
        "url": "https://nodesh01.bdcashprotocol.com",
        "ip": "134.122.56.67"
    },
    {
        "pubkey": "03b2131eef9abc87f7f1fd29b3a27c4fb9add53884ece96a4ad7696f86f5e2a168",
        "url": "https://nodesh02.bdcashprotocol.com",
        "ip": "104.248.93.57"
    },
    {
        "pubkey": "03b2131eef9abc87f7f1fd29b3a27c4fb9add53884ece96a4ad7696f86f5e2a168",
        "url": "https://nodesh03.bdcashprotocol.com",
        "ip": "134.122.58.161"
    }
]
```

In this case we asked the smart contracts to return all the nodes in which it is active and therefore where we can query it.

## [POST] /contracts/pin

This is an administration function and is used to *hook* a smart contract to an IdaNode. The call must always be signed and the message must contain only the address of the contract to be connected.

The signature must clearly be done by the same private key inserted inside the node, inside the `.env` file in the` NODE_KEY` parameter.

The call will look like this:
```
{
  "message": "8cD7AGaY74xvVxDg3NkKjfP6QpG8Pmxpnu",
  "hash": "bcd92f448766b7d5284670390382e56d55d91d25e9c261ef3a67e8b950583ca3",
  "signature": "ac3e69be1d8752ff3e2c45054c3fd949e642a4522469e2c9d2ae22ee5edca3d0707296e592512f9ae9a52443fbcaf004fe82bc19b7a70caafbe6c244a079fd57",
  "pubkey": "03b2131eef9abc87f7f1fd29b3a27c4fb9add53884ece96a4ad7696f86f5e2a168",
  "address": "8aoH8mrMgKoE7Egte8WuhMPpBeBJJHnT7M"
}
```

This endpoint will produce a blockchain write, it is therefore necessary to have a minimum of 100 BDCASH within the node address.

## [POST] /contracts/unpin

Same method of use; it is used to cancel the previous call.