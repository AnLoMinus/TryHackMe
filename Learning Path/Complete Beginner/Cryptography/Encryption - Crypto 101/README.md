![image](https://user-images.githubusercontent.com/51442719/172149395-d4648ee5-4264-4598-9319-b43bda4b5b06.png)
- [x] [Encryption - Crypto 101](https://tryhackme.com/room/encryptioncrypto101)
  > An introduction to encryption, as part of a series on crypto
    - [x] Task 1  What will this room cover?
    - [x] Task 2  Key terms
    - [x] Task 3  Why is Encryption important?
    - [x] Task 4  Crucial Crypto Maths
    - [x] Task 5  Types of Encryption
      - `Symmetric encryption` uses the same key to encrypt and decrypt the data. 
        - Examples of Symmetric encryption are DES (Broken) and AES. 
        - These algorithms tend to be faster than asymmetric cryptography, and use smaller keys (128 or 256 bit keys are common for AES, DES keys are 56 bits long).
      - `Asymmetric encryption` uses a pair of keys, one to encrypt and the other in the pair to decrypt. 
        - Examples are RSA and Elliptic Curve Cryptography. 
        - Normally these keys are referred to as a public key and a private key. 
        - Data encrypted with the private key can be decrypted with the public key, and vice versa. 
        - Your private key needs to be kept private, hence the name. 
        - Asymmetric encryption tends to be slower and uses larger keys, for example RSA typically uses 2048 to 4096 bit keys.
      - `RSA` and Elliptic Curve cryptography are based around different mathematically difficult (intractable) problems, which give them their strength.
        -  More about RSA later.    
    - [x] Task 6  `RSA` - Rivest Shamir Adleman
      - There are some excellent tools for defeating RSA challenges in CTFs 
        - [RsaCtfTool](https://github.com/Ganapati/RsaCtfTool)
        - [RsatTool](https://github.com/ius/rsatool)
        - [RSA ENCRYPTION](https://muirlandoracle.co.uk/2020/01/29/rsa-encryption/)
      - The key variables that you need to know about for RSA in CTFs are p, q, m, n, e, d, and c.
        - “p” and “q” are large prime numbers, “n” is the product of p and q.
        - The public key is n and e, the private key is n and d.
        - “m” is used to represent the message (in plaintext) and “c” represents the ciphertext (encrypted text).
    - [x] Task 7  Establishing Keys Using Asymmetric Cryptography
    - [x] Task 8  Digital signatures and Certificates
    - [x] Task 9  SSH Authentication
    - [x] Task 10  Explaining Diffie Hellman Key Exchange
    - [x] Task 11  PGP, GPG and AES
    - [x] Task 12  The Future - Quantum Computers and Encryption

---

#  Key Terms
- `Ciphertext` - The result of encrypting a plaintext, encrypted data
- `Cipher` - A method of encrypting or decrypting data. Modern ciphers are cryptographic, but there are many non cryptographic ciphers like Caesar.
- `Plaintext` - Data before encryption, often text but not always. Could be a photograph or other file
- `Encryption` - Transforming data into ciphertext, using a cipher.
- `Encoding` - NOT a form of encryption, just a form of data representation like base64. Immediately reversible.
- `Key` - Some information that is needed to correctly decrypt the ciphertext and obtain the plaintext.
- `Passphrase` - Separate to the key, a passphrase is similar to a password and used to protect a key.
- `Asymmetric encryption` - Uses different keys to encrypt and decrypt.
- `Symmetric encryption` - Uses the same key to encrypt and decrypt
- `Brute force` - Attacking cryptography by trying every different password or every different key
- `Cryptanalysis` - Attacking cryptography by finding a weakness in the underlying maths
- `RSA` - Rivest Shamir Adleman
- `PGP` - Pretty Good Privacy
- `GPG` - GNU Privacy Guard
- `AES` -  Advanced Encryption Standard

# Private-key cryptosystems
> Private-key cryptosystems use the same key for encryption and decryption.
- Caesar cipher
- Substitution cipher
- Enigma machine
- Data Encryption Standard
- Twofish
- Serpent
- Camellia
- Salsa20
- ChaCha20
- Blowfish
- CAST5
- Kuznyechik
- RC4
- 3DES
- Skipjack
- Safer
- IDEA
> Advanced Encryption Standard, also known as AES and Rijndael.

# Public-key cryptosystems
> Public-key cryptosystems use a public key for encryption and a private key for decryption.
- Diffie–Hellman key exchange
- RSA encryption
- Rabin cryptosystem
- Schnorr signature
- ElGamal encryption
- Elliptic-curve cryptography
- Lattice-based cryptography
- McEliece cryptosystem
- Multivariate cryptography
- Isogeny-based cryptography

---

# Sources


