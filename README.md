# openssl-cheatsheet
OpenSSL Cheat Sheet

## Generate keys
### Generate RSA Private Key (AES Encrypted PEM)
$ openssl genrsa -aes256 -out key1-priv-rsa2048.pem 2048
$ openssl genrsa -aes256 -out key1-priv-rsa2048.pem 4096


### Generate P12 file (just private key no certs)
$ openssl pkcs12 -export -aes256 -macalg sha256 -out key1.p12 -inkey key1-priv-rsa2048.pem -nocerts 


## Export / Decrypt 
### Decrypt encrypted private key
$ openssl rsa -in secured.pem -out clear.pem

### Export Public Key
$ openssl rsa -in key1-priv-rsa2048.pem -outform pem -pubout -out key1-pub-rsa2048.pem 

### Export Private Key from P12 file
$ openssl pkcs12 -in key1.p12 -nocerts -out myprivkey.pem

### Export certs from P7B file
$ openssl pkcs7 -inform pem -outform pem -in chain.p7b -print_certs > chain.pem
$ cat chain.pem | awk 'split_after==1{n++;split_after=0} /-----END CERTIFICATE-----/ {split_after=1} {print > "cert" n ".pem"}'



## View / Inspect Certs /CRLs
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


## Convert to different formats
### .pem => .pk8
$ openssl pkcs8 -topk8 -inform PEM -outform DER -nocrypt -in pem-private-key.pem -out pk8-private-key.pk8


## Verify
trust.pem is one or many trusted CA certs in pem format.  full chain is generally needed
mycert.pem is cert to verify
$ openssl verify -verbose -CAfile trust.pem mycert.pem







