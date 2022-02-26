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
