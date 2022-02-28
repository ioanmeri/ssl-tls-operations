# SSL communication

## Overview

1. Authentication (Handshake)

   (Public Key Algo)

2. Key Exchange (Handshake)

   (PublicKey Algo / Key Exchange Protocol)

3. Encrypted data transfer (Record)

   (PrivateKey Algo - purely symmetric, faster and encrypted data transfer)

The first two steps are collectively called SSL handshake protocol, which authenticates the server and decide on a symmetric / shared key for the actual data transfer

The third step is the actual encrypted data transfer, which is called **SSL Record Protocol**

SSL requires **both symmetric** and **asymmetric algorithms** with an optional key exchange algorithm

## Step 1. Authentication

**Through SSL Certificate**

- RSA Certs
- 2048 bits to be safe

Client sends a **client hello message** to the server that contains:

- Highest SSL version is supports (SSLv3, TLS 1.0, TLS 1.1, TLS 1.2)
- Ciphers suite Supported in that version
- Data Compression Methods
- Session id = 0
- Random Data (for entropy)

### Cipher Suite

Cipher is a string of max 6 parts:

**TLS(1)\_ ECDHE(2)\_RSA(3)\_WITH_AES256(4)\_CBC(5)\_SHA(6)**

1. The transport layer protocol use

   (others: SSL)

2. Session key exchange algorithm

   (others: RSA (public key algo), DH, DHE)

3. PKI type of the Certificate

   (others: DSS)

4. Symmetric algorithm used to encrypt the actual data

   (others: RC4, 3DES, CAMELLIA, ARIA, DES40)

5. Mode in which the symmetric algorithm operates

   (others: CCM, GCM)

6. Hashing algorithm for data integrity

   (others: MD5, SHA2)

The server prepares a **server hello** message:

- Selected SSL Version
- Selected Cipher Suite
- Selected Data Compression Method
- Assigned Session Id, Random Data

  Also:

- **Server Certificate**
- **(Client Certificate Request)**
- **Server Hello Done**

The client now verifies Server cert and checks cipher parameters.

An invalid certificate mostly means MITM attack

If server requested a client cert, the client sends the certificate to the server and server validates it.

## Step 2. Key Exchange

**RSA Method**

- Most used (XX%)

- Uses servers public key for confidentiality while exchanging secret

- No Perfect Forward Secrecy **(PFS)** and hence passive cryptanalysis is possible

- Server's private key, critical point of compromise

**Diffie Hellman Method**

- Most efficient and **recommended**

- Ephemeral mode for PFS. Blast radius of passive cryptanalysis limited to a session

## Key Exchange Mechanism - Diffie Hellman

How Diffie Hellman Protocol resolves the common secret without actually sending any PMS across the wire.

- Whitfield Diffie and Martin Hellman in 1976
- No long term private key involved
- DHE provides Perfect Forward Secrecy
- No secret key is exchanged

1. Sharing a common number which is not a secret

2. Each of them uses it's own secret key, not shared ever, on the common number to create a unique intermediate key

3. Client and server interchange keys through internet in plain text

4. Each of them uses the original private key, and does the same operation in other's intermediate key just received. The result is a pre-mastered secret

Pre-mastered key calculated on client and server **will be the same**

DH being ephemeral means: the secret keys of client and the server changes for every session. Breaking it to one session has impact only on that particular session - no session recorded in the past can be decrypted

**Discrete Logarithm Problem (in - integer domain - Zp\*)**

Even though a, p, A and B are known to the adversary, calculating

```
a = log(a)A mod p
```

is practically impossible with 'p' being a large prime number
