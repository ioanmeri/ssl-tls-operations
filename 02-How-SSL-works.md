# How SSL works

- CA's root certificate
- Website's Domain certificate

## How it works

1. **Certificate Authority** (CA e.g. Symantec, Godaddy..) publishes its root (or public) certificate to all browser vendors (e.g. Mozilla, Google..)

- CAs use public key infrastructures to cryptographically sign the certificates for the various requesting domains
- A CA has it's own private - public key pair. Public key is available for everyone publicly.

---

2. **CA's root certificate is distributed** as part of the browser application

- Browser Vendors (e.g. Mozilla, Google for Chrome, Apple for Safari) make sure that all the browsers in the market have a copy of CAs public keys, bundled as part of the application
- When the user downloads the browser, he gets all the CA's public keys in by default
- This is necessary for browser to verify the certificates signed by a particular CA

---

3. **Certificate Signing Request**

- When you want to enable SSL for your website, **you find a CA of your choice and you send a request** which has many mandatory fields **to verify that your are the owner** of the website

---

4. **Signed Certificate**

- CA signs the request
- A digital signature is nothing but the checksum of something encrypted with it's private key
- **CA calculates the checksum of the certificate and encrypts the checksum using CA's own private key**, which is only known to the CA
- The system administrator of the web server adds it to the web server configuration

---

5. **Request for webpage**

- User's browser initiates an **SSL handshake**

---

6. **SSL certificate for the website**

- Web server responds with SSL certificate for the domain of the website

---

7. **Verify**

- Browser reads the certificate to find the CA that signed the certificate
- and look up for that particular CA's public key in it's own trust store
- It **decrypts the signature** to get the checksum string
- It also calculates the checksum of the received certificate separately and then compares the result with the decrypted value of checksum
- If they match the checksum that the CA had when it was signed and the checksum that is calculated by the browser from the certificate we get a green secure lock

## CA Signed vs Self Signed Certificates
