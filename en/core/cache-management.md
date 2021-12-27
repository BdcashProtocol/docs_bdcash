# Cache management

## clearCache()

Clears the temporary cache that is generated when creating transactions. It is not mandatory to invoke this method and does not provide any visible response.

## returnTXIDCache()

This method returns the transaction cache and can be used to generate consecutive unconfirmed transactions on the blockchain. This method is invoked internally.

## pushTXIDtoCache(txid)

Insert a TXID into the cache. This method is invoked internally.

## returnUTXOCache()

This method returns the UTXO cache and can be used to generate consecutive unconfirmed transactions on the blockchain. This method is invoked internally.

## pushUTXOtoCache(utxo)

This method places a UTXO inside the cache. This method is invoked internally.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMzODg5MDk0M119
-->