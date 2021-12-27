# Local development

To develop locally we need a couple of essential tools and a little patience to configure everything.
First make sure you have [NodeJS] (https://nodejs.org/en/download/) installed (we recommend version 14).
We also recommend having Docker installed to proceed with a quick installation of the IdaNode locally.

If we have NodeJS we can proceed to install the requirements:

- Virtual Machine: https://github.com/BdcashProtocol/bdcash-vm

- NOdeSH: https://github.com/BdcashProtocol/bdcash-nodesh

### Install ScryptaVM

The following command will globally install the virtual machine, make sure you have permission to do so with `sudo` or its equivalent:

```
sudo npm install -g @bdcash-protocol/vm
```

### Install IdanodeJS

The simplest thing to install the NodeSH is to use Docker:

```
git clone https://github.com/BdcashProtocol/bdcash-nodesh
cd bdcash-nodesh
bash docker/docker.sh
```

This will install the IdaNode. As soon as everything is ready you can test with `cURL` or go directly with the browser to http://localhost:3001.

```
curl http://localhost:3001/wallet/getinfo
```

## Prepare the local folder

First of all we recommend to fully clone [this] (https://github.com/BdcashProtocol/bdcash-smart-contracts) repository that contains a series of test Smart Contracts and the necessary to start everything without errors:

```
git clone https://github.com/BdcashProtocol/bdcash-smart-contracts
cd bdcash-smart-contracts
npm install
```

After installing everything we can proceed with starting the local playground by typing the command:
```
bdcash-contracts start &
```

For contract modification we recommend using an IDE such as Atom. Recall that although the contract files have the extension `ssc` they are still very similar to javascript files. This means that any `linter` might tell you that there are errors. It is therefore preferable to use an editor that does not force you to do so.

We are therefore ready to write and interact with our contract!

## Read a contract

To test a contract it is sufficient to use a command like:

```
bdcash-contracts read -m=helloworld.ssc
```

## Test a contract

To test a contract it is sufficient to use a command like:

```
bdcash-contracts test -f=helloworld -p='{"me": "alan"}' -m=helloworld.ssc -i=SsmVKf8eb8ME3Bhrs3GPELuLjoKYcvrwkigDBocAi7pbiCdprve3
```

The possible parameters are as follows:
- f: the function we want to start
- p: the parameters to be sent (it is possible to send both objects and strings)
- m: the path of the contract
- i: the private key of the identity that must interact with the contract, if not entered, the system creates one automatically

## Publish a contract

To publish a contract it is sufficient to use a command like:

```
bdcash-contracts publish -m=helloworld.ssc -i=SsmVKf8eb8ME3Bhrs3GPELuLjoKYcvrwkigDBocAi7pbiCdprve3
```


## Make the contract available

To make the contract available on the network you simply have to sign the address of your contract (which in the previous case is `8dS3uF52kzdq3qnv8jgsAb8MnMLqVnZjnB`) with the same identity present in the NodeSH and write the same message in the blockchain.

To do this, simply write a command like:

```
bdcash-contracts pin -c=8dS3uF52kzdq3qnv8jgsAb8MnMLqVnZjnB -i=SsmVKf8eb8ME3Bhrs3GPELuLjoKYcvrwkigDBocAi7pbiCdprve3
```

where `c` is the address of the contract,` i` the private key present on your (or your) NodeSH.
Congratulations, your contract is online!

You are now ready to interact with the contract using the [playground online] (https://playground.bdcashprotocol.com) or by writing your frontend using [`@bdcash-protocol/core`] (/core/interaction-smart-contracts).

## Remove the contract from the network

If for some reason you want to remove the contract from the network it will be enough to give a command similar to the one before, only we will have to write `unpin`:

```
bdcash-contracts unpin -c=8dS3uF52kzdq3qnv8jgsAb8MnMLqVnZjnB -i=SsmVKf8eb8ME3Bhrs3GPELuLjoKYcvrwkigDBocAi7pbiCdprve3
```