# BDCash Smart Contracts

In the BDCash Blockchain, Smart Contracts are considered to all intents and purposes as *an extension* of the NodeSH, useful for creating additional features.

Inside the NodeSH the npm module `@bdcash-protocol/vm` is called which allows you to create a virtual trustless environment and which allows the smart contract to execute code inside the host machine.

Here the link to the BDCash Virtual Machine repository: https://github.com/BdcashProtocol/bdcash-vm

## Disclaimer: what BDCash Smart Contracts are and what they are not
BDCash Smart Contracts are not directly inspired by Ethereum Smart Contracts. Consequently, BDCash's approach to Smart Contrats cannot be the same as with Ethereum.

## What BDCash Smart Contracts are not
- They are not Ethereum Smart Contracts
- They are not automatically hosted in all nodes of the network (NodeSHs)
- They cannot manage LYRA funds or hold private keys
- They do not write information on behalf of the user but it is the user who writes information within the blockchain: the smart contract can *validate* information and maintain its status or be recalled from a data written directly in the blockchain by the user
- They are not a single entity (smart contracts coexist in all the NodeSHs that replicate them and can only agree on the status in a given block)

## What BDCash Smart Contracts are
- They are really automatic, that is, they self-execute each block or upon receipt of information in the mempool
- They are immutable but updatable, i.e. the code is immutable (because it is publicly displayed within a transaction) but can be updated by publishing a new version. The update is entrusted to each owner of NodeSH.
- They are simple, they are written with Javascript and expose their methods through the NodeSH.
- Although they cannot write on behalf of the user, they can * generate * formally valid transactions and delegate the signature and broadcast to the user.
- They have `consent` features whereby each client can ask if that node is trusted or not.

Having clarified these basic concepts we can start we can proceed with the explanation of the [BDcash Virtual Machine] (/smart-contracts/bdcash-virtual-machine).