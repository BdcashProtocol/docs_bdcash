# Encrypt-Decrypt Data

## cryptData(data, password)

This method uses the algorithm **AES-256** to encrypt a string of information, and return the hexadecimal representation of it.
```
let string =  'Some super secret'

let password =  'AReallyStrongPassword!!'

const bdcash = new BDCashCore

let encrypted =  await bdcash.cryptData(string, password)

/*

 Answer:

 befba636e2212846bf1c15ff4ef9e5a17ac3e6f1ce3935f4639849d44b8c9565 

*/
```
## decryptData(data, password)

This method decrypts a previously encrypted string and returns its original content. It will return `false` in case of wrong password.
```
let hex =  'befba636e2212846bf1c15ff4ef9e5a17ac3e6f1ce3935f4639849d44b8c9565'

let password =  'AReallyStrongPassword!!'

const bdcash = new BDCashCore

let decrypted =  await bdcash.decryptData(hex, password)

/*

 Answer:

 Some super secret

*/
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIyMjgwNTEyN119
-->