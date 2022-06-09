# Glossary of cryptographic keys

From Wikipedia, the free encyclopedia

[Jump to navigation](#mw-head) [Jump to search](#searchInput)

Wikipedia glossary

This glossary lists types of [keys](</wiki/Key_(cryptography)> "Key (cryptography)") as the term is used in [cryptography](/wiki/Cryptography "Cryptography"), as opposed to [door locks](</wiki/Key_(lock)> "Key (lock)"). Terms that are primarily used by the U.S. [National Security Agency](/wiki/National_Security_Agency "National Security Agency") are marked _(NSA)_. For classification of keys according to their usage see [cryptographic key types](/wiki/Cryptographic_key_types "Cryptographic key types").

- **40-bit key** - key with a [length of 40 bits](/wiki/40-bit_encryption "40-bit encryption"), once the upper limit of what could be [exported](/wiki/Export_of_cryptography "Export of cryptography") from the U.S. and other countries without a license. Considered very insecure. _See_ [key size](/wiki/Key_size "Key size") for a discussion of this and other lengths.
- **authentication key** - Key used in a keyed-hash message authentication code, or [HMAC](/wiki/HMAC "HMAC").
- **benign key** - (NSA) a key that has been protected by encryption or other means so that it can be distributed without fear of its being stolen. Also called **BLACK key**.
- **content-encryption key (CEK)** a key that may be further encrypted using a KEK, where the content may be a message, audio, image, video, executable code, etc.
- **crypto ignition key** An NSA key storage device ([KSD-64](/wiki/KSD-64 "KSD-64")) shaped to look like an ordinary physical key.
- **cryptovariable** - NSA calls the output of a [stream cipher](/wiki/Stream_cipher "Stream cipher") a key or key stream. It often uses the term **cryptovariable** for the bits that control the stream cipher, what the public cryptographic community calls a [key](</wiki/Key_(cryptography)> "Key (cryptography)").
- **data encryption key (DEK)** used to encrypt the underlying data.
- **derived key** - keys computed by applying a predetermined [hash algorithm](/wiki/Hash_algorithm "Hash algorithm") or [key derivation function](/wiki/Key_derivation_function "Key derivation function") to a [password](/wiki/Password "Password") or, better, a [passphrase](/wiki/Passphrase "Passphrase").
- **DRM key** - A key used in [Digital Rights Management](/wiki/Digital_Rights_Management "Digital Rights Management") to protect media
- **electronic key** - (NSA) key that is distributed in electronic (as opposed to paper) form. _See_ [EKMS](/wiki/EKMS "EKMS").
- **[ephemeral key](/wiki/Ephemeral_key "Ephemeral key")** - A key that only exists within the lifetime of a communication session.
- **expired key** - Key that was issued for a use in a limited time frame ([cryptoperiod](/wiki/Cryptoperiod "Cryptoperiod") in NSA parlance) which has passed and, hence, the key is no longer valid.
- **FIREFLY key** - (NSA) keys used in an NSA system based on [public key cryptography](/wiki/Public_key_cryptography "Public key cryptography").
- **Key derivation function (KDF)** - function used to derive a key from a secret value, e.g. to derive KEK from Diffie-Hellman key exchange.\[_[citation needed](/wiki/Wikipedia:Citation_needed "Wikipedia:Citation needed")_\]
- **key encryption key (KEK)** - key used to protect MEK keys (or DEK/TEK if MEK is not used).
- **key production key (KPK)** -Key used to initialize a keystream generator for the production of other electronically generated keys.
- **key fill** - (NSA) loading keys into a cryptographic device. _See_ [fill device](/wiki/Fill_device "Fill device").
- **master key** - key from which all other keys (or a large group of keys) can be derived. Analogous to a [physical key](</wiki/Key_(lock)> "Key (lock)") that can open all the doors in a building.
- **master encryption key (MEK)** - Used to encrypt the DEK/TEK key.
- **master key encryption key (MKEK)** - Used to encrypt multiple KEK keys. For example, an HSM can generate several KEK and wrap them with an MKEK before export to an external DB - such as OpenStack Barbican.[\[1\]](#cite_note-Openstack_-_Barbican_HSM_integration-1)

- **[one time pad](/wiki/One_time_pad "One time pad") (OTP or OTPad)** - keying material that should be as long as the [plaintext](/wiki/Plaintext "Plaintext") and should only be used once. If truly random and not reused it's the most secure encryption method. _See_ [one-time pad](/wiki/One-time_pad "One-time pad") article.
- **one time password (OTP)** - One time password based on a prebuilt single use code list or based on a mathematical formula with a secret seed known to both parties, uses event or time to modify output (see TOTP/HOTP).
- **paper key** - (NSA) keys that are distributed in paper form, such as printed lists of settings for [rotor machines](/wiki/Rotor_machine "Rotor machine"), or keys in [punched card](/wiki/Punched_card "Punched card") or [paper tape](/wiki/Paper_tape "Paper tape") formats. Paper keys are easily copied. _See_ [Walker spy ring](/wiki/Walker_spy_ring "Walker spy ring"), _RED key_.
- **poem key** - Keys used by [OSS](/wiki/Office_of_Strategic_Services "Office of Strategic Services") agents in World War II in the form of a poem that was easy to remember. _See_ [Leo Marks](/wiki/Leo_Marks "Leo Marks").
- **Public/private key** - in [public key cryptography](/wiki/Public_key_cryptography "Public key cryptography"), separate keys are used to encrypt and decrypt a message. The encryption key (**public key**) need not be kept secret and can be published. The decryption or **private key** must be kept secret to maintain confidentiality. Public keys are often distributed in a signed [public key certificate](/wiki/Public_key_certificate "Public key certificate").
- **pre-placed key** - (NSA) large numbers of keys (perhaps a year's supply) that are loaded into an encryption device allowing frequent key change without refill.
- **RED key** - (NSA) symmetric key in a format that can be easily copied, e.g. _paper key_ or unencrypted _electronic key_. Opposite of _BLACK_ or _benign key_.
- **revoked key** - a public key that should no longer be used, typically because its owner is no longer in the role for which it was issued or because it may have been compromised. Such keys are placed on a [certificate revocation list](/wiki/Certificate_revocation_list "Certificate revocation list") or **CRL**.
- **[session key](/wiki/Session_key "Session key")** - key used for one message or an entire communications session. _See traffic encryption key._
- **symmetric key** - a key that is used both to encrypt and decrypt a message. Symmetric keys are typically used with a cipher and must be kept secret to maintain confidentiality.
- **traffic encryption key (TEK)/data encryption key (DEK)** - a symmetric key that is used to encrypt messages. TEKs are typically changed frequently, in some systems daily and in others for every message. See _session key_. DEK is used to specify any data form type (in communication payloads or anywhere else).
- **transmission security key (TSK)** - (NSA) seed for a [pseudorandom number generator](/wiki/Pseudorandom_number_generator "Pseudorandom number generator") that is used to control a radio in [frequency hopping](/wiki/Frequency_hopping "Frequency hopping") or [direct-sequence spread spectrum](/wiki/Direct-sequence_spread_spectrum "Direct-sequence spread spectrum") modes. _See_ [HAVE QUICK](/wiki/HAVE_QUICK "HAVE QUICK"), [SINCGARS](/wiki/SINCGARS "SINCGARS"), [electronic warfare](/wiki/Electronic_warfare "Electronic warfare").
- **seed key** - (NSA) a key used to initialize a cryptographic device so it can accept operational keys using benign transfer techniques. Also a key used to initialize a [pseudorandom number generator](/wiki/Pseudorandom_number_generator "Pseudorandom number generator") to generate other keys.
- **signature key** - [public key cryptography](/wiki/Public_key_cryptography "Public key cryptography") can also be used to electronically sign messages. The private key is used to create the electronic signature, the public key is used to verify the signature. Separate public/private key pairs **must** be used for signing and encryption. The former is called **signature keys**.
- **stream key** - the output of a [stream cipher](/wiki/Stream_cipher "Stream cipher") as opposed to the key (or _cryptovariable_ in NSA parlance) that controls the cipher
- **training key** - (NSA) un[classified](/wiki/Classified_information "Classified information") key used for instruction and practice exercises.
- **Type 1 key** - (NSA) keys used to protect [classified information](/wiki/Classified_information "Classified information"). _See_ [Type 1 product](/wiki/Type_1_product "Type 1 product").
- **Type 2 key** - (NSA) keys used to protect sensitive but unclassified (SBU) information. _See_ [Type 2 product](/wiki/Type_2_product "Type 2 product").
- **Vernam key** - Type of key invented by [Gilbert Vernam](/wiki/Gilbert_Vernam "Gilbert Vernam") in 1918. _See stream key_.
- **zeroized key** - key that has been erased (see [zeroisation](/wiki/Zeroisation "Zeroisation").)
