# IdANode management

## returnNodes()

The method returns the complete list of nodes, the answer is an array of the type:
```
['https://idanodejs01.scryptachain.org',  'https://idanodejs02.scryptachain.org',  'https://idanodejs03.scryptachain.org']
```
## checkNode(node)

It checks that the node is responding correctly. If not, it sends a `false:` response

const scrypta = new ScryptaCore

let node =  await scrypta.checkNode('https://idanodejs01.scryptachain.org')
```
/*

 Example of a positive answer:

 {"version":1000000,"protocolversion":70920,"walletversion":61000,"balance":50.55998489,"obfuscation_balance":0,"blocks":424073,"timeoffset":0,"connections":21,"proxy":"","difficulty":32391.37336531,"testnet":false,"keypoololdest":1568297083,"keypoolsize":1001,"paytxfee":0,"relayfee":0.0001,"staking status":"Staking Active","errors":"","indexed":424073,"toindex":0}

 Example of a negative answer:

 false

*/
```

## connectNode()

It combines the two previous methods by returning the first available node randomly. This node can be used to call specific functions within it.

```
const scrypta = new ScryptaCore

let node =  await scrypta.connectNode()

/*

 Answer example:

 'https://idanodejs01.scryptachain.org'

*/
```

## post(endpoint, params, node = '')

It makes a `POST` call to the first available IdANode, the list of endpoints can be found in the relevant section. This method automatically connects to the node even if it is possible to force the node and use a specific one by passing it to the `node` variable.

For example, it can be used in this way to obtain and read the data entered in the blockchain from a specific address:

```
let response = await scrypta.post('/read', { address: "LbR8m1kkLSiiTDaEU8sHeeeh1jGbGho8uo" })
```

## get(endpoint, node = '')

It makes a `GET` call to the first available IdANode, the list of endpoints can be found in the relevant section. This method automatically connects to the node even if it is possible to force the node and use a specific one by passing it to the `node` variable.

For example, it can be used in this way to obtain and read wallet data.

```
let response = await scrypta.get('/wallet/getinfo')
```
