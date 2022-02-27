# Certificate Architecture

## Structure of certificate

Signature section is added by CA after signing the Data section with it's private key

It is the signature that browser reads and verifies the Data section of the certificate

Data

- Version
- Serial number
- Signature Algorithm
- Issuer
- Validity
  - Start date
  - End date
- Subject's Pub Key
- X509 Extensions
  - SAN (Subject Alternative Name)
  - CRL/OCSP ... etc.

Signature

- Signature Algorithm
- Signature

### X509 Extensions

**Subject Alternative Name: SAN**

List of domain names, for which this particular certificate is valid. If the administrator install the certificate on any of those DNS entries, it can be verified by the browser

**Authority Information Access**

- CA Issuers - URI: http://pki.google.com/GTAG2.crt

  This is a way to get the intermediate CAs certificate from online, if e.g. browser doesn't find it in trust store

- OCSP: Open Certificate Status Protocol

  A way to check weather if the cert is valid, in case the owner revoked the certificate

**X509v3: Basic Constraints: critical**

- CA: FALSE
  It will take the value false, if it is not a root certificate (public certificate of a CA). If false, it is leaf cert

**X509v3 CRL Distribution Points:**

URI:...
CRL is the certificate's revoke list

## Digital Signature

In general, a digital signature is the hash of something signed with the private key of the signer.

The data input file can be a document, video, software etc..

The digital signature is sent along with the original content of the file. Users verify integrity and authenticity of the message.

### Steps for a sender to send a signed document

1. Sender calculates the **hash**(digest) of the input, using a Hashing Algorithm like SHA2

2. Sender encrypts the hash using Sender's Private Key - **Signing**

3. The resulting signature and the original document are send together to the receiver

4. Receiver decrypts the signature using Sender's Public Key that is available publicly - **hash**

5. Receiver calculates the **hash**(digest) of the input

6. Receiver compares both the hashes - **Signature verification**

- If they match => The integrity of the document is verified.
- If they are different => the document is either tampered or the public key is wrong.

> Receiver knows what hashing algorithm was used to calculate the signature because it is a plain text information send along with the signature

### Overview on Digital Signature

- Hash of something signed by private key

- Verified using public key

- Satisfies Integrity, Authenticity and Non-repudiation

- Verification is done by comparing the message digests (Hashes)

- Applications - SSL, Secure eMail, eDocuments, Watermarking

## Certificate standard and encoding methods

**Standard**

- x509 - PKIX (Public Key Infrastructure) certificate - rfc6818
- One of the _ITU X.500 Directory standards_ was chosen to be the certificate standard for SSL by NetScape when they designed SSL. So, what are colloquially known as SSL certificates are actually "X.509 certificates".

**Encoding**

- DER (Distinguished Encoding Rules) Std => Binary DER encoded certs. (appear as .cer/.crt files)
- PEM (Privacy Enhance Mail) Std => ASCII (Base64) armored data prefixed with a "--- BEGIN ---" line. (appears as .cer/.crt/.pem files)

**File extensions**

.crt => \*nix convention of binary DER or (ASCII) Base64 PEM

.cer => Microsoft convention of binary DER or Base64 PEM

.key => public/private PKCS#8 keys. DER or PEM.

```
# Encoding conversion
> openssl x509 -in ServerCertificate.cer -outform der -out ServerCertificate.der

> openssl x509 -in ServerCertificate.der -inform der -outform pem -out ServerCertificate.pem
```

When you request the CA for certificate, the CA may sign and give you back a DER or PEM standard certificate.

If we can read the content, is PEM encoded.

## Types of certificates

based on **trust level (DV, OV, EV)**

### DV - Domain Validated (Basic)

- Small or medium level website owners who only wish to encrypt their domain can issue DV SSL certificate
- Features
  - No paper work or documentation required for validation. Validated against the domain. It does not guarantee the identity of the website's owner nor the actual existence of the organization
  - Green padlock
  - Lower price
  - Quick issuance within minutes
  - 99.9% mobile and web browser compatibility
  - Comes up with Wildcard and Multi Domain features
  - Reissue as many times as needed during the validity period
- Validation process(email, file, registrar)
- https://aboutssl.org/domain-validated-ssl-validation-process

In certificate details, the owner:

> This website does not supply ownership information

### OV - Organization Validated (Enhanced)

- Business identity level trust. Organization name printed in the certificate.

- Features

  - Green padlock
  - 1 - 3 days for issuance
  - More trusted than DV
  - Organization name is validated and part of the certificate. (Organization and Subject are filled up)

- https://aboutssl.org/document-require-for-ov-ssl-code-signing-certificate

### EV - Extended Validated (Complete)

- For trusted and high security sites

- Features

  - Green address Bar + Organization Name + Trust Seal
  - Up to 10 business days for issuance & Very Strict Validation Process
  - OV by default + High 256-bit encryption with 2048-bit Key Length
  - Multi domain with SAN only.

- https://aboutssl.org/document-require-for-ev-ssl-certificate
