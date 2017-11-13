# Usage:
<br>

### 1. Creating the Root CA certificate:
<br>

    $ ./createRootCA
<br>
   This creates your own **Root CA** and enables your organization to issue certificates to use into your internal/peers projects and test labs.
<br><br>

### 2. Creating certificate sign requests (csr):
<br>
Creates the sign request and prompts you to specify all x509 required fields according to your needs.  *If you already have a (.csr) file, skip this step* :
<br><br>

    $ ./csr <fqdn>

   e.g.: ```$ ./csr www.domain.com```

 <br>
  
   **(hint)**: If you need to generate **WildCard** requests from some domain, use the ```-w``` parameter:

<br>

    $ ./csr -w <domain fqdn>



   e.g.: ```$ ./csr -w domain.com```, to create a request for **\*.domain.com**.

<br>

**(hint 2)**: It will fill the Full Qualified Domain Name (fqdn) into the **x509 Common Name** and **DNS** fields, as required by RFC 2818 and prevent `NET::ERR_CERT_COMMON_NAME_INVALID` browsers warning.

<br><br>

### 3. Issuing a certificate signed by our root CA:

<br>

Now it is time to sign the request using our CA:

<br>

    $ ./issue <fqdn>



   e.g.: ```$ ./issue foo.domain.com```

<br>

   **(hint)**: notice that it requires a certificate sign request provided by step 2.

<br><br>
### 4. Revoking an issued certificate:

<br>

If you notice that, for some reason, an issued certificate has been compromised (lost its private key confidentiality, for example), there is no reason to trust it anymore so, revoke it:

<br>

    $ ./revoke <certificate file>

   e.g.: ```$ ./revoke ./certs/foo.domain.com/foo.domain.com.cer```

<br>

   **(hint)**: The revoked certificate appears at ```./CA/crl/ca.crl``` file. Don't forget to **make it public** for peer information.
 
<br><br>

# TODO:

* Add MultiSAN certificate easy generation support.
* Add a configuration file to set default parameters like key size, cipher suite algorithms, etc and improve maintenance.

<br><br>

# Changelog:

**Nov-2017:**
* Now all issued certificates are stored at ```./certs/\<fqdn\>``` for clearness and to follow OpenSSL standards.

* Also, the CA file structure is also following default OpenSSL, as indicated in openssl.conf.

* Introducing Certificate Revocation List features.
Now it is possible to revocate any certificate issued by mini-PKI-tools and this procedure completes the mini-PKI-tools suite. Please check ./CA file structure.

* When creating the Root CA it is required to specify the default parameters from CSR generation, to make it easy if you generate all the same structure.

* In each certificate directory, there is 3 verification files (checkCert, checkCSR and checkKey) to easy verification. Just type:

<br>

    $ checkCert
    $ checkCSR
    $ checkKey

<br>

to see its content. 

<br>

This way, it not necessary to check ```./conf``` files for default values. The createRootCA procedure fill default values when create Root CA. But, it doesn't hurt to check it again. :D

**Jun-2017:**
* Launching mini-PKI-tools basic features.

<br>

# mini PKI tools:

<br>

mini PKI tools is a set of **OpenSSL-based** Bash scripts (running Linux only), an its objective is to

    provide a set of tools to simplify the task of create, issue and revoke x509 compliant digital certificates. 

<br>

All certificates issued by mini PKI are already X509 **V3** (RFC 2818) compliant, so forget about

`NET::ERR_CERT_COMMON_NAME_INVALID`

```SubjectAltName``` Chrome browser error.

<br>

For your convinience, it also converts the **certificates into PEM (.pem) and PKCS12 (.pfx) files**, so you don't have to worry about convert your certs anymore.

<br><br>

```
Author: Daniel Avelino  <daavelino@gmail.com>

License: Creative Commons ShareAlike 4.0.

Release: Jul-2017
Rev 0.2: Nov-2017
```
<br><br>
