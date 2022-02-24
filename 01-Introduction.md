# SSL / TLS Operations

## Content

1. Introduction

2. How SSL works?

3. Structure of SSL Certificate

4. Encryption Algorithms

5. SSL Communication

6. Certificate provisioning

7. OpenSSL - Library and CLI

8. Chain of trust

9. Trust stores

10. Journey to TLS 1.3

11. Advanced topics

## Why do we need SSL certificates ?

1. **Source identity verification**

   Is it really mybank.com that I am accessing? (Trust)

2. **Security against Man-in-the-middle(MITM)**

   Can someone see my credit card number on the net? (Confidentiality &Integrity)

3. **Client/Server authentication**

   Can server identify the client back as well?

4. **Non-Repudiation**

   Can mybank.com repudiate the actions later?

## SSL/TLS Evolution

- The Secure Sockets Layer (SSL) Protocol was developed by Netscape in 1994; in response to the growing concern over security on the Internet

- Taher Elgamal & Kipp Hickman

- SSL certificate is produced as proof of identity in SSL protocol

- Transport Layer Security (TLS) protocol was created by Internet Engineering Task Forc (IETF) as the successor to SSL. TLS is based on SSL. RFC2246(TLS 1.0)

| SSL/TLS Version   | Life time   |
| ----------------- | ----------- |
| SSL 1.0           | 1994 - 1995 |
| SSL 2.0           | 1995 - 2011 |
| SSL 3.0           | 1996 - 2015 |
| TLS 1.0 (SSL 3.1) | 1999 -      |
| TLS 1.1           | 2006 -      |
| TLS 1.2           | 2008 -      |
| TLS 1.3           | 2018 -      |
