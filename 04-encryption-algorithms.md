# Encryption Algorithms

## Introduction to Encryption Algorithms

**Kerckhoff's Principle**

A cryptosystem should be secure even if the attacker knows all details about the system, with the exception of the secret key. In particular, the system should be secure when the attacker knows the encryption and decryption algorithms.

- Private/Symmetric Key Encryption Algorithms

- Public/Asymmetric Key Encryption Algorithms

- Hashing Algorithms

**Symmetric/Private Key Algorithms**

| Key Length               | Security Estimation                                                                                                                          |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| 56-64 bits (AES, 3DES)   | Short term: a few hours/ days                                                                                                                |
| 112-128 bits (AES, 3DES) | Long term: several decades without Quantum computing. Months / Years with powerful quantum computing algorithms up to 5 years down the line. |
| 256 bits (AES, 3DES)     | Long term: several decades even with Quantum computing computers with powerful quantum computing algorithms up to 5 years down the line      |

**Asymmetric/Public Key Algorithms**

Algorithm Family, Security Estimation & Key Length

| Algorithm Family                      | Few hours /days | Decades w/ QC | Decades w/o QC |
| ------------------------------------- | --------------- | ------------- | -------------- |
| Integer Factorization (RSA)           | 1024 bits       | 3072 bits     | 15360 bits     |
| Descrete Logarithm (DH, DSA, Elgamal) | 1024 bits       | 3072 bits     | 15360 bits     |
| Elliptic Curves (ECDH, ECDSA)         | 160 bits        | 256 bits      | 512 bits       |

## Private / Symmetric Key Encryption

**Private** meaning there is only one key involved and it is private to both parties involved in the secure communication

**Symmetric** meaning that encryption and decryption are using the same key. Both parties should known the secret key in advance. Key exchange should be done by other means (mail, word of mouth, messages)

- DES, 3DES, AES, RC4
- Based on single common shared secret key
- Faster than Public Key encryption
- Both sender and receiver should have the shared secret

### Flow

1. The sender encrypts the input data with the secret key and sends it across the receiver.

2. The receiver uses the same shared key, which has been communicated to him previously, by some other means, to decrypt the message

If the shared secret key is compromised the safe communication fails

## Private / Symmetric Key Encryption - AES

Advanced encryption standard

- Based on Rijndael algorithm
- Block cipher
- Modes
  - Electronic Codebook (ECB)
  - Cipher Block Chaining (CBC)
  - Output Feedback (OFB)
  - Counter (CTR)
  - Galois / Counter Mode (GCM) - Recommended over others
- 128, 192 and 256 bits
