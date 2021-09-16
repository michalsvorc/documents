# GnuPG

* [User guides](https://www.gnupg.org/documentation/guides.html)
* [GnuPG - ArchWiki](https://wiki.archlinux.org/title/GnuPG)
* [GnuPG Frequently Asked Questions](https://www.gnupg.org/faq/gnupg-faq.html#glossary)

Primary key must be capable of making signatures.

Deleting user IDs and subkeys on your own key, however, is not always wise since it complicates key distribution. By
default, when a user imports your updated public key it will be merged with the old copy of your public key on his ring
if it exists. The components from both keys are combined in the merge, and this effectively restores any components you
deleted. Consequently, for updating your own key it is better to revoke key components instead of deleting them. See
https://www.gnupg.org/gph/en/manual.html#AEN305

## Concepts

A symmetric cipher is a cipher that uses the same key for both encryption and decryption.

In a public-key system, each user has a pair of keys consisting of a private key and a public key. GnuPG uses a somewhat
more sophisticated scheme in which a user has a primary keypair and then zero or more additional subordinate keypairs.
The primary and subordinate keypairs are bundled to facilitate key management and the bundle can often be considered
simply as one keypair.

A primary key must be capable of making signatures.it is possible to later add additional subkeys for encryption and
signing.

### Key size

The longer the key the more secure it is against brute-force attacks, but for almost all purposes the default keysize is
adequate since it would be cheaper to circumvent the encryption than try to break it. Also, encryption and decryption
will be slower as the key size is increased, and a larger key size may affect signature length. Once selected, the key
size can never be changed.

### Expiration date

For most users a key that does not expire is adequate. The expiration time should be chosen with care, however, since
although it is possible to change the expiration date after the key is created, it may be difficult to communicate a
change to users who have your public key.

### User ID

A user ID should be created carefully since it cannot be edited after it is created.

### Revocation certificate

After your keypair is created you should immediately generate a revocation certificate for the primary public key using
the option --gen-revoke. 

A revoked public key can still be used to verify signatures made by you in the past, but it cannot be used to encrypt
future messages to you. It also does not affect your ability to decrypt messages sent to you in the past if you still do
have access to the private key.

Since the certificate is short, you may wish to print a hardcopy of the certificate to store somewhere safe such as your
safe deposit box. The certificate should not be stored where others can access it since anybody can publish the
revocation certificate and render the corresponding public key useless.

## Public keys

* [Manual](https://www.gnupg.org/gph/en/manual/x56.html)

## Validation

Once a public key is imported to your public keyring it should be validated. GnuPG uses a powerful and flexible trust
model that does not require you to personally validate each key you import. 

A key is validated by verifying the key's fingerprint and then signing the key to certify it as a valid key. A key's
fingerprint is verified with the key's owner. After checking the fingerprint, you may sign the key to validate it. 

Once signed you can check the key to list the signatures on it and see the signature that you have added. Every user ID
on the key will have one or more self-signatures as well as a signature for each user that has validated the key.

## Encrypting and decrypting documents

* [Manual](https://www.gnupg.org/gph/en/manual/x110.html)

A public key may be thought of as an open safe. When a correspondent encrypts a document using a public key, that
document is put in the safe, the safe shut, and the combination lock spun several times. 

The corresponding private key is the combination that can reopen the safe and retrieve the document. In other words,
only the person who holds the private key can recover a document encrypted using the associated public key.

To encrypt a document the option --encrypt is used. You must have the public keys of the intended recipients.

If you want to encrypt a message to Alice, you encrypt it using Alice's public key, and she decrypts it with her private
key. In particular, you cannot decrypt a document encrypted by you unless you included your own public key in the
recipient list.

## Symmetric encryption (passphrase only)

Documents may also be encrypted without using public-key cryptography. Instead, only a symmetric cipher is used to
encrypt the document. The key used to drive the symmetric cipher is derived from a passphrase supplied when the document
is encrypted, and for good security, it should not be the same passphrase that you use to protect your private key.

## [Digital signature](https://www.gnupg.org/gph/en/manual/x135.html)

A digital signature certifies and timestamps a document. A signature is created using the private key of the signer. The
signature is verified using the corresponding public key.

### Signed document

The command-line option [--sign](https://www.gnupg.org/gph/en/manual/r606.html) is used to make a digital signature. The
document to sign is input, and the signed document is output.

The document is compressed before signed, and the output is in binary format. Given a signed document, you can either
check the signature or check the signature and recover the original document.

### Clearsigned documents

The option [--clearsign](https://www.gnupg.org/gph/en/manual/r684.html) causes the document to be wrapped in an
ASCII-armored signature but otherwise does not modify the document.

### Detached signatures

A signed document has limited usefulness. Other users must recover the original document from the signed version, and
even with clearsigned documents, the signed document must be edited to recover the original.

 Therefore, there is a third method for signing a document that creates a detached signature. A detached signature is
 created using the [--detach-sig](https://www.gnupg.org/gph/en/manual/r622.html) option.

Both the document and detached signature are needed to verify the signature. The --verify option can be to check the
signature.

