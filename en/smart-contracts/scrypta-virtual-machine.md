# BDCash Virtual Machine

## Abstract

BDCash was born from a fork of PIVX and rests its blockchain foundations directly on the concepts of Bitcoin (being PIVX a fork of Dash, which in turn is a fork of Bitcoin). Consequently, within the BDCash blockchain there is no reference to the concept of Smart Contracts as they are commonly imagined.

Although we strongly believe that decentralized applications do not largely need Smart Contracts, on the other hand, we realize that there are many other applications that need to work with a highly decentralized and highly scalable logic. That said, we started thinking about the possibility of allowing third party developers to use our "backend" technology, that is the NodeSH, without actually corrupting them or having to act directly inside the source code.

Until now, all the applications that required to interact with an "additional" logic had to create new projects that interact with the NodeSH, thus leaving the maintenance of particular logics to other software.

After a careful analysis of the various existing Smart Contracts platforms, we tried to define the "qualities" that our system should have:
- **Scalability:** the system must be highly scalable, ensuring stability in the use of the platform as its use increases.

- **Automatism:** the system must be able to "self-execute" itself or perform certain actions in a totally automatic way.

- **Simplicity:** the system must give the developer ease of development without having to learn new programming languages.

- **Upgradability:** the system must guarantee the updating of the software while maintaining its immutability.

We believe that the system designed can actually satisfy all the above requirements, in the next paragraphs we will explain how.

## NodeSH, VM and compiler

At the basis of the functioning of the platform we have three entities:

- **NodeSH:** used to interact with the blockchain in reading and writing, they will allow the execution of the Smart Contract and will keep the status of the Smart Contract in its database, based on the interactions and rules written at the inside the code.

- **Virtual Machine:** the virtual machine (VM2) allows you to execute code * "untrusted" * or * host * of the IdaNode and is the safe environment in which the code is executed. The Virtual Machine has a few, predefined, internal modules available and interacts with the IdaNode database limited to its own sphere of competence or a collection of the database.

- **Compiler:** although Smart Contracts are written in Javascript, the compiler allows you to * translate * certain predefined rules (such as reading and writing the database) into a native language capable of communicating with the IdaNode.

## IdaNode Modules

The modules are the most important part. Although we can continue to call them "Smart Contracts" in fact the platform allows you to create * modules / extensions * for the IdaNode. These modules are * enabled * within the IdaNode and therefore by one or more specific NodeSH. Hence the first point in our list of required features: *scalability*.

Modules are not natively included in all NodeSH but only in those that have * the interest * to keep them and therefore * the interest * to provide more or less computing power for their execution.

This means that a specific application can be maintained only by its creator or by all those interested in using it and therefore means that the number of interested parties will grow with the increase in users and that consequently the system will always have computing power to provision to serve different users.

This type of approach has already been used in decentralized applications such as IPFS or Torrent.

## Clock and automation

The specific interaction with the NodeSH allows to solve another big problem encountered in other Smart Contracts platforms, namely automatisms. While it is generally accepted that the Smart Contract "executes itself on the basis of specific rules", this idea is drastically wrong.

Taking the example of Ethereum, a Smart Contract may eventually "automatically" have conditions such that `if` executed (and we repeat the * if *), it will lead to a change of state within it.

This is because the Ethereum Virtual Machine does not have a real `clock` which is a fundamental characteristic of all electronic * machines * and which allows synchronization by means of a certain * cycle *. In computers, for example, it is calculated in Hertz (GHz) and defines the quantity to perform operations that the computer can perform every second.

Clearly, to extend the concept of *clock* to the blockchain we must abstract from the concept related to computers and think that the *clock* of the VM (i.e. the moment when the machine synchronizes) is the emission of a block, which in the BDCash network is about 1 minute.

This means that we can think of having our Smart Contract execute *at least* one operation every block, that is when a "cycle" has been concluded.

We have therefore created the basis for the automatisms, all Smart Contracts can call the `eachBlock` function and **auto-execute** of the code regardless of whether someone invokes or does not invoke the Smart Contract itself.

You can also call the `eachMempool` function to" listen "for information inside the mempool itself.

## Immutability and updatability

Speaking of blockchain and Smart Contract we can only mention one of the fundamental characteristics that the code must have: immutability.

Immutability is guaranteed by the blockchain as the code is not directly executed from a file, but this file must first be loaded into an address, thanks to the techniques we know. The code executed by the VM and by the user is therefore well defined and static and we have the guarantee that the code has been published by its author thanks to a double signature process.

However, any software during its * life * needs updates and this is a fact. Thanks to the * Progressive Data Management * technique applied also in the tool [`bdcash-BVC`] (/utilities/versioning-cli) it is possible to update the source code of the Smart Contract thus publishing corrective and / or functional modification versions.

This feature is however optional and is defined at the first deployment of the Smart Contract.

## Interaction with the Smart Contract

The IdaNode allows you to interact with the contract by means of a specific API that exposes the methods written within the contract or by writing the calls that you want to execute within the contract directly in the blockchain. The latter mode will clearly make the action immutable as it is written in the blockchain.