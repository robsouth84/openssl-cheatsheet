# openssl-cheatsheet
OpenSSL Cheat Sheet



### View DER Certificate
$ openssl x509 -inform der -in mycert.der -text 

### View certificate CRL Distribution Point (CDP)
$ openssl x509 -inform der -in mycert.der -text | grep URI 

### View CRL
$ openssl crl -inform pem -text -in mycrl.pem 
$ openssl crl -inform der -text -in mycrl.crl 

### Convert CRL from DER to PEM
$ openssl crl -inform der -text -in mycrl-DER.crl -out mycrl-PEM.pem



