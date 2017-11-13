# Usage:

### 0. Get the required files:
<br>
Just type:
<br>

    $ git clone https://github.com/daavelino/mini-pki-tools.git
<br>
or 
<br>

    $ wget https://github.com/daavelino/mini-PKI-tools/archive/master.zip
<br>

or use the [Clone or Download](https://github.com/daavelino/mini-PKI-tools/archive/master.zip) github page.
<br>

### 1. Creating the Root CA certificate:
<br>
It all starts by creating your own Root Certification Authority. This enables you to sign certificates and set up a trust network based on it:
<br>

    $ ./createRootCA

   Now you own a **Root CA** and is apt to issue certificates to use into your internal/peers projects and test labs.
<br>

### 2. Creating certificate sign requests (csr):
<br>
To properly issue a certificate, some information must to be provided in order to identify it with your organization and needs.

<br>
<br>

>Special attention to **Common Name** field, since it must be the same as **Full Qualified Domain Name** if you are issue a Web certificate.
<br>

If your intention is to issue a certificate to a **www.domain.com** address, **remember to set Common Name as www.domain.com**.

Otherwise, web browsers (and other User-Agents) will not recognize it properly.
 
If you already have a (.csr) file, skip this step: 
<br>

    $ ./csr <fqdn>

   e.g.: ```$ ./csr www.domain.com```

<br>

   **(hint)**: If you need to generate **WildCard** requests from some domain, use the ```-w``` parameter:
<br>

    $ ./csr -w <domain fqdn>


   e.g.: ```$ ./csr -w domain.com```, to create a request for **\*.domain.com**.

<br>

**(hint 2)**: It will fill the Full Qualified Domain Name (fqdn) into the **x509 Common Name** and **DNS** fields, as required by RFC 2818 and prevent `NET::ERR_CERT_COMMON_NAME_INVALID` browsers warning.
<br>

### 3. Issuing a certificate signed by our root CA:
<br>
Now it is time to sign the request using our CA:

<br>

    $ ./issue <fqdn>



   e.g.: ```$ ./issue foo.domain.com```

<br>

   **(hint)**: notice that it requires a certificate sign request provided by step 2.

<br>
### 4. Revoking an issued certificate:
<br>
If you notice that, for some reason, an issued certificate has been compromised (lost its private key confidentiality, for example), there is no reason to trust it anymore so, revoke it:

<br>

    $ ./revoke <certificate file>

   e.g.: ```$ ./revoke ./certs/foo.domain.com/foo.domain.com.cer```
<br>

   **(hint)**: The revoked certificate appears at ```./CA/crl/ca.crl``` file. Don't forget to **make it public** for peer information.
<br>
# TODO:

* Add MultiSAN certificate easy generation support.
* Add a configuration file to set default parameters like key size, cipher suite algorithms, etc and improve maintenance.

<br>
# Changelog:

**Nov-2017:**
* Now all issued certificates are stored at ```./certs/\<fqdn\>``` for clearness and to follow OpenSSL standards.

* Also, the CA file structure is also following default OpenSSL, as indicated in openssl.conf.

* Introducing Certificate Revocation List features.
Now it is possible to revocate any certificate issued by mini-PKI-tools and this procedure completes the mini-PKI-tools suite. Please check ./CA file structure.

* When creating the Root CA it is required to specify the default parameters from CSR generation, to make it easy if you generate all the same structure.

* In each certificate directory, there is 3 verification files to easy visualization of their content. Just type:


    $ checkCert
    $ checkCSR
    $ checkKey

<br>
into ```./certs/<fqdn>``` directory to see if everything is ok. 
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

<br>
```
Author: Daniel Avelino  <daavelino@gmail.com>

License: Creative Commons ShareAlike 4.0.

Release: Jul-2017
Rev 0.2: Nov-2017
```
<br><br>
