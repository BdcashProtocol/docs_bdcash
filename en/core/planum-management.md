# Planum Transaction Management

This section will describe how to use Planum technology, i.e. how to manage transactions, unspents etc.

## usePlanum(sidechain)

The first thing to do to operate with Planum and ScryptaCore technology is to choose the reference sidechain, so that the instance knows where to get the data.

We then choose the sidechain with which we want to operate, for example:`6Kk2jkJ76wjZiBvDr6j1R9Ub9z9TWXBK18`

```
const scrypta = new ScryptaCore
scrypta.usePlanum('6Kk2jkJ76wjZiBvDr6j1R9Ub9z9TWXBK18')
```

## verifyPlanum()

It allows you to check the status and consent of a sidechain within the established network. It is recommended to use this feature in conjunction with `scrypta.staticnodes = true` as requesting consent from an extended network can be a lengthy operation. Setting the `staticnodes` property to` true` prompts the client to connect only to the `mainnetIdaNodes` or` testnetIdaNodes` nodes. By default `idanodejs01 ... 06`.

## listPlanumUnspent(address, safe = false)

It allows to obtain the list of "unspent" (USXO) of a specific address. The response contains an array of USXOs that will be used to construct the transactions.

Usually this method is invoked internally but can be used to check for example the address balance.

The `safe` parameter allows you to take into account only confirmed unspents, which is recommended in most cases.

## sendPlanumAsset(key, password, to, amount, changeaddress = '', memo = '', time = '', safe = false, inputs = [])

This is the primary method for sending transactions. It internally invokes all the methods listed above.

The parameters are described below:

-   **key:** iThe identity payload to use.

-   **password:** the password to decrypt the identity payload.
        
-   **to:** the receiving address.
    
-   **amount:** the amount of tokens to send.

-   **changeaddress:** any exchange address, if different from the departure one.
    
-   **memo:** any text string to be written in the transaction.
    
-   **time:** the timestamp of the transaction, by default the Proof of Timestamp smart contract is used, a pre-established timestamp can be used as an alternative, to block the tokens until the chosen date. It is important to understand that all outputs will be blocked, so it is better to use an intermediate address from which to send the tokens "in the future".
    
-   **safe:** allows you to determine whether to use only confirmed inputs

-   **inputs:** allows you to establish which inputs to use, very useful in the case of sending NFTs (which notoriously refer to a specific input)
    

## returnPlanumBalance(address)

Returns the balance of the requested address. The answer will also return any balance blocked in the future with respect to the time of the request.

## returnPlanumTransactions(address)

Returns the list of transactions of the requested address.