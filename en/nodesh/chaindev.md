# Chain Dev Platform

The BdcashProtocol Sidechain protocol is described in the appropriate section. In this section we will show how to interact with Sidechains through the IdANode enpoints.

## [POST] /sidechain/issue

This endpoint is used to create a Sidechain, the internal processes of which are described in the "Issuance" chapter of the dedicated section. We recommend creating a new personal address directly from Web Wallet, so that we can manage the tokens via the graphical interface. It is required to have at least **100 BDECO** in the balance of the address, otherwise the creation will not be successful.

Here are the data fields to use to create a new Sidechain:
- **dapp_address**: the owner address of the sidechain
- **private_key**: Private key of the owner's address
- **pubkey**: public key of the owner's address
- **version**: the protocol version is currently `1`
- **name**: descriptive name of the sidechain
- **symbol**: sidechain alphanumeric ticker
- **supply**: the amount of tokens to be created
- **decimals**: the number of decimals of the token
- **burnable**:  it can be `true` or` false`. Determines whether or not the token can be sent to the trustlink address to perform a token burn.
- **reissuable**: it can be `true` or` false`. Determines whether the token is fixed supply or can be reissued later.
- **permissioned**: can be `true` or` false` and determines if the sidechain is permissioned or not, if set to `true` all users must be authorized.
- **extendable** (WIP): can be `true` or` false` and determines if the token is extended by a smart contract or not (still in work in progress, do not use).

If the operation is successful, the new sidechain will be displayed here: https://devs.bdcashprotocol.com and the available balance will also be visible.


## [POST] /sidechain/reissue

This endpoint is used to reissue tokens within an existing sidechain. This process can only be done by the sidechain owner and only if it has been marked as `reissuable`.

These are the information to be sent for token reissue:
- **dapp_address**: The owner's address
- **sidechain_address**: The sidechain address
- **private_key**: The owner's private key
- **pubkey**:The owner's pubkey
- **supply**: The amount of tokens to be reissued

The response received will contain the information necessary to verify that everything went well. Subsequently this new reissue transaction will be displayed in the unspent list.

## [POST] /sidechain/send

Through this enpoint you can send the tokens in your possession to another address. To do this, the following fields must be sent:

- **from**: the address from which you want to send the tokens
- **private_key**: the private key of the address that sends the tokens
- **pubkey**: the public key of the address that sends the tokens
- **sidechain_address**: the address of the sidechain
- **to**: the address that will receive the tokens
- **amount**: the amount to be sent. Remember to respect the division of decimals as the IdANode rounds the figure to make sure of the accuracy of the operation. Any difference will result in the sending of a rounded amount, therefore different from the one requested.

The answer is very similar to that of writing any other data:

```
{
	
	"uuid":  "9ae3751c.5448.46df.adf3.07626213bc01",

	"address":  "LdRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2",

	"fees":  0.011000000000000003,

	"collection":  "",

	"refID":  "",

	"protocol":  "chain://",

	"dimension":  771,

	"chunks":  11,

	"stored":  "*!*9ae3751c.5448.46df.adf3.07626213bc01!*!!*!!*!chain://*=>{\"transaction\":{\"sidechain\":\"8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH\",\"inputs\":[{\"sxid\":\"c623e7d599b335bd60f3ca371824ea0882bad80173f76e8d1c454173b4fca763\",\"vout\":1,\"address\":\"8dRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2\",\"amount\":99080.5986,\"sidechain\":\"8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH\",\"block\":482119}],\"outputs\":{\"LMnX7FrofprX5UY5M1KjsYAdhkCVL5vR1i\":18,\"8dRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2\":99062.5986},\"time\":1574700620860},\"signature\":\"037595724e395b1c01472871f542465c3264299f7c079d477d21c6d0a75e8c177f9ac99c73d38c680f189ab543be02e951656e6a76913adc45e93fd59f512d43\",\"pubkey\":\"027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0\",\"sxid\":\"8db6cf7c0de249607d8771b12f318ae7c7173eb965b675e55fcb807f96e4186a\"}*!*",

	"txs":  [

		"bd8415460b31d4fad510b1f2f3e41ee410c1240935774489f16352378fd004f6",

		"49029166c852ff00a5215ee95020bfd5c20e770adccfe3fa44c1508de84df797",

		"c433fcba4fb2c59262feb3b2f07aca8a48b69c0abdafe38e609b16af70ffa1b1",

		"08d32aa928d40980fa10ab662e3512b2090ad1bc9c256673b2c60199e0ac2bfc",

		"2e8295fa1a5dcd47370aefe33cc7ff4941abd37d0d67846fe442d46a266a8806",

		"18f9f72a1a8c30e326bf3937886443db9d36530f218f2bbb3b32729913c8e402",

		"416490028397c5bd221af56e87e6529b6520ab0a2409c980ea280950ffbd3d68",

		"7f42b6698494d2057ad96ec9dd09ad65d09547a13ee839a1f7619b07c309b7d8",

		"c4dcc0d68131ebcc3cfaa0cbe12141055caf6903d527d2967a261316a1d53002",

		"fe9ce2fe695e8c99e969c3f14382c7b56d13bd681f5b38337355b30e2c7f3b62",

		"f81feaaf0a2fea766dacc97bbf060b214cfe435578ce42d2dc460da8e96022a5"

	]

}
```

## [POST] /sidechain/balance

This operation allows you to view your balance at a specific sidechain. The following fields must be sent:

- **dapp_address**: the BdcashProtocol address you want to inspect
- **sidechain_address**: address to sidechain.

The answer will be similar to the following:
```
{

	"balance":  99062.5986,

	"symbol":  "TST",

	"sidechain":  "8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH"

}
```

## [POST] /sidechain/shares

It allows you to view all the active wallets inside the sidechain and check the balance and weight inside the sidechain itself. The total supply including any reissues and burned token is also reported.

The answer will look like this:
```
{
    "shares": {
        "8dRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2": {
            "balance": 800,
            "shares": 80
        },
        "8Yghqiod3pb3NStSMWLShntiFrcnVrdEwo": {
            "balance": 200,
            "shares": 20
        }
    },
    "cap": 1000,
    "burned": 0,
    "sidechain": "8TbMDNr3Nnnpi4H6F3EMzU25FkWVz6quLE"
}
```

## [POST] /sidechain/transactions

It allows you to view transactions made from an address at a specific sidechain. The following fields must be sent:
The answer will look like this:

- **dapp_address**: the BDECO address you want to inspect
- **sidechain_address**: the address of the sidechain.

The answer will look like this:

```
{

	"transactions":  [

		{

		"sxid":  "5aa7b97e1b22eec134781af42d11501f0701b771451dda9be4361b5a0f07eaa1",

		"from":  "8dRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2",

		"to":  "8chzGX6vqmanceCzNUMTk5cmnt1p6knGgT",

		"amount":  10,

		"block":  482075

		},

		{

		"sxid":  "0ac9210cd4dbd08550a1ca7501ed7336c6ee1e0700791518ff7c3bdbaa0db22f",

		"from":  "8chzGX6vqmanceCzNUMTk5cmnt1p6knGgT",

		"to":  "8NmYWqaU5qrZcHxCA2vVTMmvKcaXBdjKUZ",

		"amount":  -50,

		"block":  482061

		},

		{

		"sxid":  "ac6b491fa140464427b3cb933796a4820d22a454d125d6e744b7fcce8b6acac5",

		"from":  "8chzGX6vqmanceCzNUMTk5cmnt1p6knGgT",

		"to":  "8RJRsP9ZhszTNAmtubwiSzzLFGn4DfZZcU",

		"amount":  -150,

		"block":  481989

		}

	],

	"symbol":  "BDUST",

	"sidechain":  "9RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH"

}
```

## [POST] /sidechain/listunspent

It allows you to view spendable transactions (**USXO**) from an address at a specific sidechain. The following fields must be sent:

- **dapp_address**: the BdcashProtocol address you want to inspect
- **sidechain_address**: the address of the sidechain.

Answer example:
```
	{

	"unspent":  [

	{

		"sxid":  "8db6cf7c0de249607d8771b12f318ae7c7173eb965b675e55fcb807f96e4186a",

		"vout":  1,

		"address":  "8dRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2",

		"amount":  99062.5986,

		"sidechain":  "8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH",

		"block":  482413

	}

	],

	"sidechain":  "8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH"

}
```

## [POST] /sidechain/scan/address

It allows you to view all the sidechains with balance for a specific address.

- **dapp_address**: the BdcashProtocol  address you want to inspect

The answer will look something like this:
```
{

	"data":  [

	{

		"sidechain":  "8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH",

		"symbol":  "BDUSD",

		"balance":  555

	}

	],

	"status":  200

}
```


## [GET] /sidechain/list

It allows you to view all the sidechains created and valid within the BdcashProtocol network.

Answer example:
```
{

	"data":  [

		{

			"genesis":  {

			"name":  "BdcashProtocol  USD",

			"supply":  100000,

			"symbol":  "BDUSD",

			"decimals":  "8",

			"reissuable":  "false",

			"owner":  "8dRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2",

			"pubkey":  "027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0",

			"version":  "1",

			"time":  1574499539348

		},

		"signature":  "ad6af516d89d9610e17296d10b63d2bd26bb34cd29157860f8d68314f469b2dd521d16c969d8fbd9af5b377b18095f9716b1f1de782662f33d74f585295d210e",

		"pubkey":  "027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0",

		"sxid":  "325179d9602bd342c2e5fa15771d5f1490e519f2560eef752bf5c9a6f592cdd5",

		"address":  "8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH"

		},

		{

		"genesis":  {

			"name":  "BdcashProtocol  Bitcoin",

			"supply":  1,

			"symbol":  "BDBTC",

			"decimals":  "0",

			"reissuable":  "false",

			"owner":  "8bj39Vysy4YUuAct9Yo2hFnETApQKV8EfK",

			"pubkey":  "02e40a0edd697bf59c38b26903f7f46401d312b4fac8fc3989ea0753db64444fbd",

			"version":  "1",

			"time":  1574679790587

		},

		"signature":  "12154510cde6d5179025ccb1176c1ec1fa486b57cbe80e6679a7bd46003f62517f1925e62a466abf9ff8c4ed2971021b8f7058ae4aa161d0562d134c5a967c2a",

		"pubkey":  "02e40a0edd697bf59c38b26903f7f46401d312b4fac8fc3989ea0753db64444fbd",

		"sxid":  "cb9c15f37b340b6988adee38a0175abe366325abeb21459bae6e97ab195c767d",

		"address":  "8WmU2zVLvDRkxHmqkiSETRmm89HtM2y4Wj"

		}

	],

	"status":  200

}
```


## [POST] /sidechain/get

Return the sidechain object.

- **sidechain_address**: the address of the sidechain you want to inspect

## [POST] /sidechain/verify

Check the entire sidechain from the beginning of the chain and verify that each transaction is valid. It is used to remove any double spend or other errors.

- **sidechain_address**: the address of the sidechain you want to inspect

## [POST] /sidechain/scan

It allows you to view all the transactions of a specific sidechain.

- **sidechain_address**: the address of the sidechain you want to inspect

Answer example:
```
{
	
	"data":  [

	{

		"transaction":  {

		"sidechain":  "8WmU2zVLvDRkxHmqkiSETRmm89HtM2y4Wj",

		"inputs":  [

		{

		"sxid":  "8903dd2cc9428a0a879c7ee43376657d6a93a95f2d94830751eee5d9bb10fb4f",

		"vout":  0,

		"address":  "8chzGX6vqmanceCzNUMTk5cmnt1p6knGgT",

		"amount":  1,

		"sidechain":  "8WmU2zVLvDRkxHmqkiSETRmm89HtM2y4Wj",

		"block":  482128

		}

		],

		"outputs":  {

		"8RJRsP9ZhszTNAmtubwiSzzLFGn4DfZZcU":  1

		},

		"time":  1574698567404

	},

	"signature":  "1574c802484602234d0be73992f673d24526cd0580a64c3243e3680f2cd34c681164edc704344bc330979629732efb8921576e6d948ca482c539f259c9eb553d",

	"pubkey":  "030249ca95b9d10701d9dfb08cb43b79ee229c3c621a9d17b84320b61690e87d09",

	"sxid":  "baca71e1fb87faacca7b772b0c2ecaf3de13bcba4501b7a980bcda49d1dac484",

	"block":  482383

	},

	{

		"transaction":  {
		
			"sidechain":  "8WmU2zVLvDRkxHmqkiSETRmm89HtM2y4Wj",

			"inputs":  [

			{

			"sxid":  "992ba66c6cf9c1b4bd8375d9525909020ab9ebd208173e36547e1ae5581b2f3d",

			"vout":  0,

			"address":  "8bj39Vysy4YUuAct9Yo2hFnETApQKV8EfK",

			"amount":  1,

			"sidechain":  "8WmU2zVLvDRkxHmqkiSETRmm89HtM2y4Wj",

			"block":  482071

			}

			],

			"outputs":  {

			"8chzGX6vqmanceCzNUMTk5cmnt1p6knGgT":  1

			},

			"time":  1574683028721

		},

		"signature":  "972de254a686f1358c5de2c7ddd4a28da0e8b41e02f3c55971e97d10ff67911327a9335380575bd24cee5894ea3ee55ec4503f2a309cbf8d0fbc684d4625d08f",

		"pubkey":  "02e40a0edd697bf59c38b26903f7f46401d312b4fac8fc3989ea0753db64444fbd",

		"sxid":  "8903dd2cc9428a0a879c7ee43376657d6a93a95f2d94830751eee5d9bb10fb4f",

		"block":  482128

		},

		{

		"transaction":  {

		"sidechain":  "8WmU2zVLvDRkxHmqkiSETRmm89HtM2y4Wj",

		"inputs":  [

		{

		"sxid":  "cb9c15f37b340b6988adee38a0175abe366325abeb21459bae6e97ab195c767d",

		"vout":  "genesis"

		}

		],

		"outputs":  {

		"8bj39Vysy4YUuAct9Yo2hFnETApQKV8EfK":  1

		},

		"time":  1574679790945

	},

	"pubkey":  "02e40a0edd697bf59c38b26903f7f46401d312b4fac8fc3989ea0753db64444fbd",

	"signature":  "b87e2de54fe6b8676c60b7fc050c39f7357c6cb863c088e40a8bb1222a54ab0422c64c89ff8892a6b8942168c2c87894672d3edcf964b0f018730aee5f6ff6a2",

	"sxid":  "992ba66c6cf9c1b4bd8375d9525909020ab9ebd208173e36547e1ae5581b2f3d",

	"block":  482071

	}

	],

	"status":  200

}
```


## [POST] /sidechain/transaction

Allows you to view a specific **SXID**.
 
The following fields must be sent:
- **sxid**: the id of the transaction you want to inspect.
- **sidechain_address**: the sidechain address to which the transaction belongs.

The answer will look like this:
```
{
	
	"transaction":  {

	"address":  "8dRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2",

	"uuid":  "99a60.a13e.4cf1.a7d9.18bf065885ee",

	"collection":  "",

	"refID":  "",

	"protocol":  "chain://",

	"data":  {

	"transaction":  {

	"sidechain":  "8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH",

	"inputs":  [

	{

	"sxid":  "60cc5945f43cf91f12b5214fb402228106003aec857f867b8ab6624d7e410f1e",

	"vout":  0,

	"address":  "8dRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2",

	"amount":  100000,

	"sidechain":  "8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH"

	}

	],

	"outputs":  {

	"8hhoDjf9pWenaAA89LqSGemr1KWBhr9uuZ":  555,

	"8dRQokR1i3XDtj1V3jnCRqMPrVc7sYkeE2":  99445

	},

	"time":  1574525110177

	},

	"signature":  "61d950526c8d381c389c899232f77eab7706aff3f2c0064768134d6c33dc53b06efb74d1483dcd9a643b1e87397164aea5e13c2c5d50c930a19416e31251bf55",

	"pubkey":  "027460a5f721e97f5e241d9767fb1b7fd778892e7c40684b79fcb4420d07d240e0",

	"sxid":  "c2f218f13325c052b16ed10a42ce5415155ec898d97fc7c8365d8cea33d4513b"

	},

	"block":  479518,

	"blockhash":  "8e616b72272143cc9f2d62bdb41d198932ecc8f3777814b1b367ec9266ae2bb5",

	"time":  1574525178

	},

	"symbol":  "TST",

	"sidechain":  "8RQ54yHx2dARWkN8Biiw3gDjb4sB5hSHSH"

}
```

## [GET] / sidechain / check /: sidechain /: extended

It allows you to do a consistency check on the sidechain. Only two parameters can be passed via URL:

- Sidechain: this is mandatory and represents the address of the sidechain itself
- Extended: this is used to perform the consistency check also with the other connected nodes (i.e. inserted in the `.env` file in the` LINKED_NODES` property) and to check the consent

This endpoint is very important in production as it allows not only to perform a formal consistency check on the sidechain (if for example the tokens issued correspond to the sum of unspent) but also allows you to check the status of the node with respect to its own "network" NodeSH.

For example calling `/sidechain/check/8ShzCp8oXAqVSZdrkNMSj13ghobwZZRzGm/true` will return a result like:
``
{
    "user_count": 6,
    "cap": 10000,
    "issued": 10000,
    "nodes": [
        "https://nodesh01.bdcashprotocol.com",
        "https://nodesh02.bdcashprotocol.com"
    ],
    "verified": true,
    "sidechain": {
        "name": "BdcashProtocol  BTC",
        "supply": 10000,
        "symbol": "BDBTC",
        "decimals": 8,
        "reissuable": true,
        "owner": "8chzGX6vqmanceCzNUMTk5cmnt1p6knGgT",
        "pubkey": "030249ca95b9d10701d9dfb08cb43b79ee229c3c621a9d17b84320b61690e87d09",
        "burnable": true,
        "version": 1,
        "time": 1582118140204,
        "address": "8ShzCp8oXAqVSZdrkNMSj13ghobwZZRzGm"
    },
    "status": "95d424632eb9ac98f1698fb260378a5e69981cb02837361f81d5ebb9a385a250",
    "users": [
        "8V5RkA9AL6ncM19RT3usKRkxd5arUS7iVt",
        "8UvRq5GygoJ4WMjiW8Zjis19jWK2mHdL2v",
        "8KbNrug6n72v52nwBFCdgK6atqh5RFBRDy",
        "8PriRhN69EKQnVPf3xYN9EWxYk3SywYbue",
        "8aoH8mrMgKoE7Egte8WuhMPpBeBJJHnT7l",
        "8chzGX6vqmanceCzNUMTk5cmnt1p6knGgq"
    ],
    "consensus": "7/7",
    "reliability": 100
}
```

As you can see, the last two properties of the object are `consensus` and` reliability` which give us the number of connected nodes that report the same status and the reliability of the node itself.

The `@ bdcash-protocol / core` library deems nodes with a value less than 50 unreliable by automatically connecting to another node accordingly.

## [POST] / sidechain / allow

It allows to enable a user to operate in the `permissioned` sidechains. The user can have two types of levels:
- `user`: that is, it can operate in receiving and sending transactions
- `validator`: that is, it can operate within the sidechain and can also ** manage ** users, just like the owner. Unlike the owner he will not be able to add other * validators *.

The following fields must be sent:
- **dapp_address**: the address you want to enable.
- **sidechain_address**: the address of the sidechain to which the user belongs.
- **private_key**: the private key you want to operate with.
- **level**: the level you want to enable, it can only be `user` or` validator`.

## [POST] / sidechain / deny

It allows you to disable, in the `permissioned` type sidechains, a user to operate.
The user must be disabled for the same level at which he was previously enabled to operate correctly as the user may have been enabled at both levels.

The following fields must be sent:
- **dapp_address**: the address you want to enable.
- **sidechain_address**: the address of the sidechain to which the user belongs.
- **private_key**: the private key you want to operate with.
- **level**: the level you want to disable, it can only be `user` or` validator`.