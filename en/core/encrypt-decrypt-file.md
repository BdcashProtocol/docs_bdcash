# Encrypt-Decrypt File

## cryptFile(file, password)

This method is used to encrypt a file, taken through an HTML input field, and returns a hexadecimal string representing the encrypted file. This string can also be quite long and the operation may take some time, depending on the size of the file itself.

The returned string cannot be sent directly to IPFS as it must first be transformed into a buffer. Later we will see an example that you can call up and use from the test interface.
```
<input  type="file"  onChange="testCryptFile(event)">
```
```
const scrypta = new ScryptaCore​

function  testCryptFile(ev){

 const file = ev.target.files[0];

 let password =  'AStrongPassword'

 let crypted = scrypta.cryptFile(file,password)

 /*

Example answer:

 e1e3a70ef671b920636e5b72f8f002024c567bd9ad5aa92d456e2306400303ac4465ee153872740984b2c08148ebcca268567c400328fad443a6a6c83326a33f274869be734b2bbce91644651f149e16a74b31947f936aca2d5835484209393d58f04efd0cf53fff57c26c23f5cb484ca4338a6a9c5a080e03179dfe6bd731e346bbdb75bcff48532e649bef90f4ad09d2ba29dd102827ba04d972bcee5fb2a0411b8815391619036dbb34fa6f05505a031cbee3fd85ff44cd575b2c4dcf7ab2d5ceb98b7e30d28e03ee25259c9b4d6b49510e0feb80469f963b6640217830ba5bb8793b0896ff4ec9ae9370d1c05371a559fbc9e822ed04ea0f541fdd4ad150837f33d5ade14341d3d6611455180cb6886941d58dacd32c8a8f7d713dc66697ea678ac789a78df247586b34f3c77aee3c6b93d56d37546bd0260886cce47190d29cd2636fec0120f4e9ee9790b4e1beb45113858d54c8196511f2d1d08014722eecc645f18aaec9af3f316cd1c47eeb1a72fa5a6ac3567d86c4bc4994012c0742359a4dd1878725462c73a76e7ad33581d0ab03711e08cf774253882f40da7c2f197ff2ecacd61284a96e8095dc736e

 */

}
```

## decryptFile(file, password)

This method decrypts a buffer, previously encrypted, and transforms it into a buffer containing the decrypted file. The method will return `false` if the entered password is incorrect.

```
const scrypta = new ScryptaCore

let encrypted =  new  Buffer('e1e3a70ef671b920636e5b72f8f002024c567bd9ad5aa92d456e2306400303ac4465ee153872740984b2c08148ebcca268567c400328fad443a6a6c83326a33f274869be734b2bbce91644651f149e16a74b31947f936aca2d5835484209393d58f04efd0cf53fff57c26c23f5cb484ca4338a6a9c5a080e03179dfe6bd731e346bbdb75bcff48532e649bef90f4ad09d2ba29dd102827ba04d972bcee5fb2a0411b8815391619036dbb34fa6f05505a031cbee3fd85ff44cd575b2c4dcf7ab2d5ceb98b7e30d28e03ee25259c9b4d6b49510e0feb80469f963b6640217830ba5bb8793b0896ff4ec9ae9370d1c05371a559fbc9e822ed04ea0f541fdd4ad150837f33d5ade14341d3d6611455180cb6886941d58dacd32c8a8f7d713dc66697ea678ac789a78df247586b34f3c77aee3c6b93d56d37546bd0260886cce47190d29cd2636fec0120f4e9ee9790b4e1beb45113858d54c8196511f2d1d08014722eecc645f18aaec9af3f316cd1c47eeb1a72fa5a6ac3567d86c4bc4994012c0742359a4dd1878725462c73a76e7ad33581d0ab03711e08cf774253882f40da7c2f197ff2ecacd61284a96e8095dc736e')

let password =  'AStrongPassword'

let decrypted =  await scrypta.decryptFile(encrypted, password)

/*

 Answer: 

 Uint8Array(419) [76, 76, 49, 99, 104, 90, 83, 71, 55, 80, 72, 110, 89, 65, 50, 101, 114, 68, 104, 97, 76, 50, 101, 54, 55, 84, 80, 49, 121, 97, 101, 54, 110, 49, 58, 99, 51, 97, 52, 56, 56, 56, 102, 100, 98, 53, 99, 97, 53, 57, 102, 101, 51, 54, 52, 53, 50, 97, 54, 51, 49, 50, 54, 51, 53, 98, 53, 99, 98, 102, 52, 48, 48, 54, 100, 51, 54, 49, 101, 99, 99, 50, 100, 99, 97, 49, 49, 51, 54, 50, 54, 48, 48, 101, 101, 55, 101, 49, 48, 102, …]

*/
```
#An example

A practical example can be found inside the Testing Suite. Here is the code to highlight the various steps that will lead to the hashing of the file with IPFS, then to the download of the same file (always through IPFS) and finally to the consequent reconstruction of the original file.
```
<input  type="file"  onChange="testCryptFile(event)">
```
```
function  testCryptFile(ev){

 const file = ev.target.files[0];

 let password =  'test'

 let isWriting =  false

 document.getElementById('cryptfileresponse').innerHTML =  'Crypting file...'

 if(isWriting ===  false){

 new ScryptaCore.cryptFile(file,password).then(crypted =>  {

 isWriting =  true

 const form_data =  new  FormData();

 form_data.append("buffer", crypted);

 console.log(crypted)

 document.getElementById('cryptfileresponse').innerHTML =  'Posting file to IPFS...'

 axios.post(

 'https://idanodejs01.scryptachain.org/ipfs/add', 

 form_data, 

 {

 "Content-Type":  "multipart/form-data"

 }).then(function  (response)  {

 console.log(response.data)

 document.getElementById('cryptfileresponse').innerHTML =  'Retrieving file from IPFS...'

 axios.get('https://idanodejs01.scryptachain.org/ipfs/buffer/'  + response.data.data[0].hash).then(ipfs =>  {

 console.log(ipfs)

 document.getElementById('cryptfileresponse').innerHTML =  'Decrypting file...'

 let data = ipfs.data.data[0].content.data

 console.log('DATA',data)

 new ScryptaCore.decryptFile(data, password).then(decrypted =>  {

 console.log('DECRYPTED', decrypted)

 document.getElementById('cryptfileresponse').innerHTML =  'Downloading file...'

 var saveByteArray =  (function  ()  {

 var a = document.createElement("a");

 document.body.appendChild(a);

 a.style =  "display: none";

 return  function  (data, name)  {

 var blob =  new  Blob(data,  {type:  "octet/stream"}),

 url = window.URL.createObjectURL(blob);

 a.href = url;

 a.download = name;

 a.click();

 document.getElementById('cryptfileresponse').innerHTML =  ''

 window.URL.revokeObjectURL(url);

 };

 }());

​

 saveByteArray([decrypted], file.name);

 })

 })

 })

 })

 }

}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAzNzUzMDQzNF19
-->