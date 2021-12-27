# Trustlink

Trustlink is a type of blockchain address, called `multisignature`, which is generated from two or more standard addresses. Multisignature addresses always start with the number `7` and standard addresses with the letter` 8`.

Aside from this alphanumeric distinction, multisignature addresses differ mainly in the method of signing transactions. Transactions must be signed by _n_ of _m_ addresses, where:
- **n:** the minimum number of required signatures required.
- **m:** the total number of addresses present.

We will see later how multisignature transactions and addresses are generated.

The BDCASH idea, which chose to call these TrustLink addresses, provides that two or more addresses that decide to sign (and therefore write) information on the blockchain are, in some way, addresses that trust each other. In our case, the necessary signatures always correspond to all the addresses present in the TrustLink. We will soon see how to use these particular addresses to sign contracts.

We are talking about *contracts* in very different terms from those usually used. The *contracts* that we mean are written agreements (or files) that are contextually signed by all participants in the Trustlink. In no case will we talk about *smart contracts*, at least not in the sense of *computer program*. The program that executes the contract, in our case, is in all respects the blockchain, through the multiple signature operation.

All operations relating to Trustlinks are carried out within the NodeSH. We will now list all the endpoints:

## [POST] /trustlink/init

This endpoint is used to generate the Trustlink starting from the public keys of the addresses that want to generate it. It is important to note that the order of public keys affects the result of the Trustlink: to facilitate the creation of always the same trustlinks between the same participants, we have decided to implement a default sorting function.

The fields to be sent will be the following:

 - **addresses**: the comma separated list containing the public address keys.
 - **airdrop**: it can be *true* or *false* and it is used to send the first initialization transaction of the amount inserted in the * .env * file of the NodeSH. By default it is **0.001 BDCASH**.

The end result will look like this:
```
{

	"data":  {

		"address":  "8ZPgAgVmd5EjYeDrWBjTXxfR2gybjVeZQo",

		"redeemScript":  "5221037794fbd3da6243079b019e15d0e2e0055b5f45825280620a7045219392d98a05210380ad898c608f92f52adec7a3c9a5bd42417218dab6d0aec60a50c299b9e0ad2052ae"

	},

	"status":  200

}
```

It is important to write down the *redeemScript* field as it is used to sign transactions in write and send operations.

## [POST] /trustlink/write

Similarly to the ** write ** endpoint for normal addresses, this endpoint allows you to write data within the blockchain.

Here is the list of possible data fields:
- **trustlink [mandatory]:** the trustlink that is writing the information.
- **data [mandatory]**: the information you want to write within the blockchain.
- **private_keys [mandatory]**: the private keys of the trustlink addresses.
- **redeemScript [mandatory]**: the same string returned in the trustlink creation operation.
- **file:** a file that can contextually be written on IPFS.
- **protocol:** the protocol to be used to classify the information.
- **collection:** the collection you want to use to classify information.
- **refID:** the reference id that you want to use to classify the information.
- **uuid:** the unique identifier assigned by the NodeSH to update a given data.

The operation is similar to that already described, therefore we recommend going to see the relevant page in the section*NodeSH > Progressive Data Management*

##  [POST] /trustlink/send

Similar to the **send** endpoint for normal addresses, this endpoint allows funds to be sent from the trustlink to another BDCASH address.

Here is the list of possible fields:
- **trustlink [mandatory]:** the trustlink that is writing the information.
- **to [mandatory]**: the Bdcash address that will receive the funds.
- **amount [mandatory]**: the amount of Bdcash to send.
- **private_keys [mandatory]**: the private keys of the trustlink addresses.
- **redeemScript [mandatory]**: the same string returned in the trustlink creation operation.
- **message:** any message to be included in the transaction. It can be a maximum of 80 bytes.

If sent successfully, the answer will look like the following
```
{

	"success":  true,
	"fees":  0.001,
	"txid":  "83f21cfff067bfb9f9002d26b9100297dc8aee8d145f8c370317349568bf3366"

}
```

## [POST] /trustlink/invalidate

It is used to invalidate a data. The parameters necessary for the operation to be successful are:
- **uuid [mandatory]:** the unique identifier returned by the NodeSH in the initial writing phase.
-  **private_keys [mandatory]:** private key of the address that wrote the information.
- **trustlink [mandatory]:** the address that wrote the information.
- **redeemScript [mandatory]:** the same string returned in the trustlink creation operation.


If sent successfully, the answer will look like the following
```
{

	"uuid":  "07ec884b.3575.4d94.a65f.5afdd5c7bd46",

	"fees":  0.001,

	"success":  true,

	"txid":  "648ceeb581b7b26897e211ff652c5adaaa878fe16a5454156d058099a7bc87e5"

}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkxNDc5MzI2MiwyMDU4MzMzNTU3LC02Mz
cxMDY3MjksMzY4Mjg5ODE2LDMyNTA5NTAwNyw4NDY1MzIzMzcs
LTIzNTY5OTAzNCwxMTc5NjI4ODEzLDEyMTc4MjU2NzQsLTE3MT
Q2NjA1NzIsLTExNzg2ODI2MTMsMTI2NzY3NTE5NiwtNjUxMjQ3
NzI4XX0=
-->