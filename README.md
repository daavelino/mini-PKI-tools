# mini PKI tools: 
a set of Linux openssl based scripts to run a mini (but functional) Public Key Infrastructure.

It is already X509 V3 SubjectAltName (RFC 2818) compliant, so forget about

`NET::ERR_CERT_COMMON_NAME_INVALID`

Chrome browser error.


It also converts the **certificates into PEM and PKCS12 (.pfx) files**, so you don't have to worry about convert your certs anymore.


```
Author: Daniel A. Avelino 

License: Creative Commons ShareAlike 4.0.

Release: Jul-2017

```

This project aims to create an internal SSL Certificate Authority, apt to sign test SSL certificates.

It will ensure a minimal level of security when deal with sensitive information transportation.

The idea is to provide an internal Public Key Infrastructure (PKI), a Root
Certification Authority and pertinent documentation to provide trust between 
this CA and PKI participants (HITSS internals).

# Usage:

1. ```./root-CA-create.bsh```

creates the Root CA certificate. 

2. ```./createRequest.bsh <fqdn>```

creates the certificate sign request for a given web address (full qualified domain name).

3. ```./issueCertificate.bsh <fqdn>```

issues a certificate signed by the root CA for a given fqdn. It requires a certificate sign request provided by createRequest.bsh.


# Optional: 

To chech the content of a certificate sign request, just do:

```$ openssl req -text -noout -in <csr file>```

and, to check the content of a certificate:

```$ openssl x509 -text -noout -in <crt file>```


# PLEASE, PLEASE, PLEASE!
Check all ./conf files to **set default values**.

For instance, to set your locality default to Sao Paulo/Sao Paulo, change the following line in the ./conf files:


```stateOrProvinceName_default 	= Sao Paulo```

```localityName_default 	= Sao Paulo```



Enjoy!
