# Technical functioning

## Introduction

Scrypta's identity system is divided into two fundamental components, the first concerns the management of strictly digital identities, that is Lyra addresses; the second concerns the authentication of addresses with external authenticators.

The first component can be handled in various ways, but basically it concerns the .sid files that we mentioned in the _Scrypta Core_ documentation. These identity payloads can be managed through:

- [**ScryptaID Browser Extension**](https://id.scryptachain.org/) (Chrome, Firefox, etc) 
 > [https://github.com/scryptachain/scrypta-id](https://github.com/scryptachain/scrypta-id)
- [**Manent Mobile App**](https://manent.app/) (iOS, Android) 
 > [https://github.com/scryptachain/scrypta-manent-app](https://github.com/scryptachain/scrypta-manent-app)
- [**Manent Web App**](https://web.manent.app/#/) (Chrome, Firefox, Mobile browser)
> [https://github.com/scryptachain/scrypta-manent-web](https://github.com/scryptachain/scrypta-manent-web)

The second component can be used through an identity gateway, such as the one that makes Scrypta available through the URL:

- [**https://me.scrypta.id/**](https://me.scrypta.id/) 
 
or through other gateways made available by other external parties.

Identity payloads, whose structure deals only with addresses, have an additional property called *identity*:

```
{

 "pub":"LLLjx7yV4nhUzSapBAHogb5BdgUR6VCB3o",

 "api_secret":"33239857dbe3d37fd35b807578a0132b",

 "key":"03097163386854cde5801aec574948e15b9e24c79da65414d4e5588e7140846165",

 "prv":"SnvpeER7kdeMFGRimBzV5EJfX2ZfxmAQwin1qAHD2kXb8XRF983g",

 "identity": {
	Provider: {
		"identity": {
			"created_at": Timestamp,
			"method": Provider,
			"username": Username,
			"token": TokenReleasedByProvider
		},
		"fingerprint": PayloadSignedByGateway
	}
  }

}
```

As we can guess, for each **Provider** (Twitter, Github, E-mail) after the correct verification by the **Gateway**, a payload is written containing:
- **created_at**: The timestamp of the operation.
- **method**: a repetition of the provider used.
- **id**: the user id at the provider.
- **username**: the username of the user with the provider.
- **token**: the token issued by the provider (which can be used for account verification).

This payload is signed by the gateway (whose private key must reside within it) and the signature is inserted into the ** fingerprint ** property.

This same payload is signed by the address that requires authentication. The signature is written within the blockchain so that it can be compared for verification with that presented by the user during the identification phase.

**N.B.** the identity payload is encrypted again and the custody is still left to the user, this to ensure decentralization and security.
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTc0OTEwMTEyLC0xNTM4OTc0ODI2LC0xNT
gwMjY0OTE0LDE1NzEzOTAzOTAsOTU0Njc2ODUzXX0=
-->

## Technical notes

The source code of the Scrypta Identity Framework, which manages the identity gateways, can be inspected at this address:

[https://github.com/scryptachain/scrypta-identity-framework](https://github.com/scryptachain/scrypta-identity-framework)

This is the component that provides interfaces to external authenticators.


**Scrypta Identity Framework** is an app developed in [**NodeJS**](https://nodejs.org). 
Providers are managed through [**PassportJS**](http://www.passportjs.org/); except for email verification, integrated via [**Mailgun**](https://www.mailgun.com/) and verification of telephone number, via [**Twilio**](https://www.twilio.com/). 


> E-mail and telephone verification takes place internally so that gateways and service providers will coincide.


## Identification confirmation

Whenever the user wants to identify himself, he must clearly show his identity payload (operation via mobile app) and the counterparty (always via the app, automatically) will verify that the payloads presented are actually valid. In essence, a verification will be carried out via public key, payload and blockchain.

The result, which can be found on the website https://me.scrypta.id, will be something like this, which we graphically render for privacy reasons:


![](/assets/idframework/proof.png)

It can actually be verified that, for example, the payload of _Github_ written to block **416667** is the following and is connected to the address `LZzzH9C7outN754hqfyTZ6Hhjk2nsoX9no`. This information can be found here: https://proof.scryptachain.org/#/uuid/3e7ce.f696.4b11.bf0c.cec51cff386e
```
{ 
	"signature": "2f04635376ef2cbbc9c083b6093e5bfc864bc779a8aa670c431f5ad14c2e261003ef2aaeaab8990f9a3cec8a67296a05b1463b5f9ba98c78d83d1269163232b7",
	"gateway": "0240f294ef20c7bbb82bae24d8d22c7ab94d195adf153162482b6bf540393d7dd5", 
	"fingerprint": "79a7c75eb20eca8ca36b781bbde1e0e960a39e4d4d92f4d4452cf47c7e5b0b936c5051690f84ee177d497003ea50dd32192cf18422130a1eb8bb6172cd48275f" 
}
```

Let's better explain what is written within the blockchain:
- **signature**: is the signature of the payload by the address `LZzzH9C7outN754hqfyTZ6Hhjk2nsoX9no`.
- **gateway**: is the public key of the gateway address.
- **fingerprint**: as mentioned, it is the signature of the same payload by the gateway address.

## Operation scheme

Here is an operating diagram that summarizes all the steps carried out:

![](/assets/idframework/funzionamento.png)

## Integrated Providers 

Currently the integrated and functioning providers are the following:
- Github
- Google
- Linkedin
- Twitter
- E-Mail
- Phone

## Final goal

The final goal of this framework is to give the possibility to entities, institutions or companies to create their own set of addresses whose identity is guaranteed thanks to the blockchain and the method mentioned above.

Scrypta is implementing this identity system within the Manent mobile app, giving users the chance to exchange identity information and save it within their "Address Book". This will allow for a double operation, the first is to be able to actually have a list of trusted contacts and the second is to create TrustLink with these contacts, so as to be able to sign agreements or sign documents.

## Extensibility and practical cases

It is clear that, for example, in the case of a company that wants to identify its employees (and their digital operations, allowing them - for example - to sign documents or interact with a corporate dApp) that the management of these payloads through files. sid (decentralized) can be cumbersome.

Thanks to the open nature of the framework, nothing prevents you from creating centralized storage for all these identities and linking them, for example, to corporate email.

Thanks to these addresses, the most varied operations can be carried out, from the exchange of funds to the signature of documents, up to the creation of trustlinks.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxOTIzNzY2MywxNjc4NjM1NTA5LDE3MT
gxMDkxODMsMTMyMTM3MTI5OSwtMjExNDEwNjAzNF19
-->