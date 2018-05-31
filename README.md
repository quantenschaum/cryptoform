# cryptoform

an end-to-end encrypted webform using PGP encryption

**This is work in progress!**


## How does it work?


### encryption

- a HTML form is displayed in the webbrowser containing several fields, textareas, file uploads
- the user fills in the form
- when the user submits the from, the following happens
- all entered data from fields and textareas is written into a text file (like JQuery's [serialize()](https://api.jquery.com/serialize/) in memory, json/yaml/xml encoded)
- the data file containing the serialized form data and all attached files are zipped together into a *single* zip file using [JSZip](https://stuk.github.io/jszip/) (in memory, nothing is uploaded yet)
- the zip file is encrypted using [kbpgp.js](https://keybase.io/kbpgp) or [openpgp.js](https://github.com/openpgpjs/openpgpjs) to one (or more) public PGP keys
- the zip file is discarded and the encrypted zip file is transmitted to the server
- the server might now forward the encrypted zip via email
- the receiver can decrypt the zip, if (and only if) in possesion of a matching private key

This should ensure end-to-end encryption. The security of participating servers and the connections between them should be irrelevant. The data is (strongly) encrypted and can safely be transmitted via unsecure connections. To prevent forgery, the form and the JavaScript code performing the encryption as well as the public PGP key **must be delivered via a secure (https) connection with headers set correctly to prevent cross site scripting**!

- The data is encrypted in the clients browser, no unencrypted data is transmitted.
- Using asymmetric cryptography ensures that only authorized persons can decrypt the data (assuming the private key beeing kept private).


### decryption

- You get a PGP encrypted zip.
- decrypt with GnuPG on the command line or via some GUI
- maybe a PGP mail client plugin handles decryption automatically
- a web based decrypter could be created
  - decryption happens in the browser using JavaScript, no data transmitted
  - drop the encrypted zip and your private key
  - "download" the decrypted zip
  

## used software/libraries

- a recent browser HTML5 appreciated
- encryption https://keybase.io/kbpgp or https://github.com/openpgpjs/openpgpjs
- key generation https://www.gnupg.org/ or https://fncontact.com/pgpkeys
- file access https://github.com/eligrey/FileSaver.js
- zipping https://stuk.github.io/jszip/
- HTML manipulation http://jquery.com/


## good to know - reading

- https://www.html5rocks.com/de/tutorials/file/dndfiles/


## key pairs

generated with https://fncontact.com/pgpkeys


## ToDo

- get prototype running
- build a library
- build a wordpress plugin

