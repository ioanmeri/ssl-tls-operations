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

## Public / Asymmetric Key Encryption

Asymmetric meaning the encryption and decryption use different keys.If you use private key for encryption, the decryption can only be done with the corresponding public key and vice versa.

- RSA, DSA
- Key bit length
- Slower

### Flow

A user has to create two keys: public key and private key

The public is shared with the entire world. Private key is only visible to it's owner. It is critical to keep the private key confidential.

### What key to use for encryption

**Confidentiality**

If you want to send an encrypted message that **is readable only by a specific receiver**, use the receiver's public key that everyone knows and send it the receiver. This message can only be decrypted only by the corresponding private key, which only the receiver has.

**Authentication**

For digital signatures, the encryption is done with the private key and the entire world can verify using the corresponding public key available to all. Everyone is able to verify that is actually signed and send by the sender.

## Asymmetric Key Algorithm - RSA

Integer Prime Factorization Problem

- Ron Rivest, Adi Shamir and Leonard Adleman in 1977
- Patent by MIT expired in 2000
- Good for signing and encryption
- Advance key computation
- Bad for key exchange

**Integer Prime Factorization Problem**

e: encryption key

d: decryption key

n: another number known publicly

m: message

For three very large positive integers e, d and n such that with modular exponentiation for all integer m:

```
(m^e)^d = m (mod n)
```

and that even knowing e and n or even m it can be extremely difficult to find d.

The public key is represented by the integers n and e; and the private key, by the integer d. An attacker wants to find d from an known n and d

## Asymmetric Key Algorithm - Elliptic Curve

- Discovered in 1985 by Victor Miller (IBM) and Neil Koblitz (University of Washington)
- Some implementations patented by Certicom
- Low computing power requirements
- Reduced key length and hence fast
- Use only standard NIST curves

**Elliptic Curve Discrete Logarithm Problem**

Let P and Q be two points on an elliptic curve such that kP = Q, where k is a scalar. Given P and Q, it is computationally infeasible to obtain k, if k is sufficiently large. k is a discrete logarithm of Q to the base P.

On Elliptic Curve, Scalar multiplication is a one way function.

## Hashing Algorithms

- One-way digest
- Unique
- Fixed length(32, 40, 64 etc.)
- Collision resistance
- MD5, SHA1, SHA2, SHA3, RIPEMD, Tiger, Whirlpool, GOST etc.

MD5 / SHA1: not collision resistant, do not use

SSL certificates use at least SHA2

Input -> hash function -> fixed size message digest

### Demonstration of collision in MD5

```
wget 2 binary files: message1, message2
```

```
openssl dgst -md5 message1.bin message2.bin
```

same output but messages are not the same. SHA1 can detect it:

```
openssl dgst -sha1 message1.bin message2.bin
```
