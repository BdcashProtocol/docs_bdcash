# P2P Network

The IdANode network is connected to a second peer-to-peer network thanks to the `socket.io` library. This allows you to send and receive cryptographically signed messages from addresses. In order to use this network it is necessary to initialize it, below all the related methods.

## connectP2P(key, password, callback)

This method allows you to connect to the network and receive any messages received thanks to the callback call. It can be used in the following way:

```
// FIRST WE CREATE A NEW ADDRESS
let password = 'ASuperStrongPassword'
let address = await scrypta.createAddress(password, true)

// CONNECT TO THE NETWORK
scrypta.connectP2P(address.walletstore, password, function(received){
    response(received)
})

// SEND A MESSAGE TO THE NETWORK
setTimeout(function(){
    scrypta.broadcast(address.walletstore, password, 'message', 'Now are '+ new Date() +'!')
},3500)
```

## broadcast(key, password, protocol, message, socketID = '', nodeID = '')

This method allows you to send messages within the network (client and IdANode) and should be used as seen previously. It is possible to customize the protocol, which is by default `message` or send to specific nodes or sockets.