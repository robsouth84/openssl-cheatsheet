# openssl-cheatsheet
OpenSSL Cheat Sheet


### Generate RSA Private Key (AES Encrypted PEM)
$ openssl genrsa -aes256 -out key1-priv-rsa2048.pem 2048
$ openssl genrsa -aes256 -out key1-priv-rsa2048.pem 4096

### Decrypt encrypted private key
$ openssl rsa -in secured.pem -out clear.pem


### Export Public Key
$ openssl rsa -in key1-priv-rsa2048.pem -outform pem -pubout -out key1-pub-rsa2048.pem 

### Generate P12 file (just private key no certs)
$ openssl pkcs12 -export -aes256 -macalg sha256 -out key1.p12 -inkey key1-priv-rsa2048.pem -nocerts 

### Export Private Key from P12 file
$ openssl pkcs12 -in key1.p12 -nocerts -out myprivkey.pem



### View DER Certificate
$ openssl x509 -inform der -in mycert.der -text 

### View certificate CRL Distribution Point (CDP)
$ openssl x509 -inform der -in mycert.der -text | grep URI 

### View CRL
$ openssl crl -inform pem -text -in mycrl.pem 
$ openssl crl -inform der -text -in mycrl.crl 

### Convert CRL from DER to PEM
$ openssl crl -inform der -text -in mycrl-DER.crl -out mycrl-PEM.pem

### Sign / Verify Files with private key
https://www.openssl.org/docs/man1.0.2/man1/pkeyutl.html


