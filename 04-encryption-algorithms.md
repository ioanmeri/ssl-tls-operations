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
