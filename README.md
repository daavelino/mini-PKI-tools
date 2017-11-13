# Usage:

1. Creating the Root CA certificate: 
```./createRootCA```


2. Creating certificate sign requests (csr) for a given Common Name [usually a web address full qualified domain name (fqdn)]:

  ```./csr <fqdn>```

  E.g.: ```./csr foo.domain.com```

  2.1. If you need to generate WildCard requests, just type:

  ```./csr -w <domain fqdn>```

E.g.: ```./csr -w domain.com```


3. Issuing a certificate signed by our root CA:

  ```./issue <fqdn>```

  E.g.: ```./issue foo.domain.com```

Notice that it requires a certificate sign request provided by step 2.


4. Revoking an issued certificate:

  ```./revoke <certificate file>```

  E.g.: ```./revoke ./certs/foo.domain.com/foo.domain.com.cer```


# TODO:

Add MultiSAN certification easy generation support.

# Changelog:

Nov-2017:
* Now all issued certificates are stored at ./certs/\<fqdn\> for clearness and to follow OpenSSL standards.

* Also, the CA file structure is also following default OpenSSL, as indicated in openssl.conf.

* Introducing Certificate Revocation List features.
Now it is possible to revocate any certificate issued by mini-PKI-tools and this procedure completes the mini-PKI-tools suite. Please check ./CA file structure.

* Now, when creating the Root CA it is required to specify the default parameters from CSR generation, to make it easy if you generate all the same structure.

This way, it not necessary to check ./conf files for default values. The createRootCA procedure fill default values when create Root CA. But, it doesn't hurt to check it again. :D

Jun-2017:
Launching mini-PKI-tools basic features.

# mini PKI tools: 
a set of Linux openssl based scripts to run a mini (but functional) Public Key Infrastructure.

It is already X509 V3 SubjectAltName (RFC 2818) compliant, so forget about

`NET::ERR_CERT_COMMON_NAME_INVALID`

Chrome browser error.


It also converts the **certificates into PEM and PKCS12 (.pfx) files**, so you don't have to worry about convert your certs anymore.


```
Author: Daniel A. Avelino  <daavelino@gmail.com>

License: Creative Commons ShareAlike 4.0.

Release: Jul-2017
Rev 0.2: Nov-2017

```

This project aims to create an internal SSL Certificate Authority, apt to sign test SSL certificates.

It will ensure a minimal level of security when deal with sensitive information transportation.

The idea is to provide an internal Public Key Infrastructure (PKI), a Root
Certification Authority and pertinent documentation to provide trust between 
this CA and PKI participants (HITSS internals).

# Validation: 

To chech the content of a certificate sign request, just do:

```$ openssl req -text -noout -in <csr file>```

and, to check the content of a certificate:

```$ openssl x509 -text -noout -in <crt file>```


Enjoy!
