# Maintenance

Maintenance of the NodeSH is essential. This is because the code, updated on a daily basis, undergoes continuous changes and improvements.

It is extremely important to regularly access NodeSH and to verify that the version is the latest available.

Each version carries with it a *checksum* to check the code, which will be compared with your NodeSH at startup.

It is essential that the * checksum * is always valid. Any unofficial modification to the code will corrupt the NodeSH and this will not allow the connection through@bdcash-prptocol/core.


### Blockchain checksum list

https://check.bdcashprotocol.com/#/address/8Q15LT7CKygxUvXB8NsnZXd3kE5xrTMfFw

### Github checksum list

https://github.com/BdcashProtocol/bdcash-nodesh/blob/master/checksum

## Update the NodeSH

To update the NodeSH run the following terminal command:

```
cd bdcash-nodesh
npm run update
```

## Create a bootstrap file

To create a bootstrap file you need to *have NodeSH active* and run the following command:

```
npm run mongodump
```

This will create the `nodesh_boostrap.gz` file which will be invoked by the script `bootstrap.sh`.