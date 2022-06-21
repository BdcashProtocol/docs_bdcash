# Playground

The playground is the easiest way to start understanding how to interact with Smart Contracts or develop new ones It can be found at this address:
[https://playground.bdcashprotocol.com](https://playground.bdcashprotocol.com/#/).

To enter the Playground it is necessary to have a BdcashProtocol identity. We recommend using the Wallet Extension, which can be found [here] (/dapps/Wallet).


## Feature overview

Upon entering the platform you will find yourself with the `Hello World` contract already in edit mode. It will then be possible to run it and interact with it using the methods shown.

On the right side you can start working on the code, which we remember to be Javascript, seeing in real time the publication or modification of a new method.

The bottom part instead shows a `console` which will return all the information necessary to understand what the virtual machine is doing.

The side menu shows the other 2 pages available, the one that shows your contracts (those you have already entered in the blockchain) and a part of "discovery" that allows you to interact with the contracts available in the network.

## Local editing

Using the first screen you can then create new local contracts. The code will be saved in the `localStorage` and will remain on your PC until you decide to publish it or _empty the cache_. If you intend to work with more confidence, we always recommend making local copies of the code or working directly locally. If you want to immediately switch to local development of smart contracts go [here] (/smart-contracts/local-development).

## Deploy a contract

As soon as you are ready to enter your contract in the blockchain you can press the green button `DEPLOY`, enter your password and wait for the confirmation of publication. From this moment on, anyone with an NodeSH can connect it using the [local development tool] (/smart-contracts/local-development#make-the-contract-available) or the appropriate [endpoint] (/nodesh/smart- contracts#post-contractspin). It is therefore _fundamental_ to have at least one own NodeSH to really put Smart Contracts on the network.

## Your own contracts

Moving to the section of your contracts we will see the addresses and the current version of each of our contracts and by clicking on the name we will enter local modification mode. By clicking the "play" icon instead we will go into execution mode.

## Discovery

Moving to the discovery section we will be able to interact with each contract entered on the network: just click the "play" icon relating to the line of the contract to enter live mode.

If, on the other hand, we want to read the contract code or use it as a "starting point" for a new local contract, by clicking on the `name` we will immediately go into local modification mode, using the published code as a basis.