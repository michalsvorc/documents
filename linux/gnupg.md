# GnuPG

- [Guides | gnupg.org](https://www.gnupg.org/documentation/guides.html)
- [GnuPG | Arch Wiki](https://wiki.archlinux.org/title/GnuPG)
- [FAQ | gnupg.org](https://www.gnupg.org/faq/gnupg-faq.html#glossary)
- [Public keys | gnupg.org](https://www.gnupg.org/gph/en/manual/x56.html)

## Create new primary key with sub keys

In this section, it is assumed that the primary key will only be used for certification and the rest of the operations (signing, authentication) are assumed to be performed using subkeys. Only in this case is it justified to extract the secret primary key and store it separately on another device (e.g. a flash drive). The primary key will only be required to create\renew keys or sign the keys of others.

Notes:
- Your primary key’s public part is still on your system, but its secret part is only on USB.
- Your encryption subkey (new or old) still has its secret part, allowing you to decrypt messages.
- If you add a new encryption subkey, both its public and secret parts are generated.

### 1. Generate new primary key

- [Gentoo Wiki](https://wiki.gentoo.org/wiki/GnuPG#Primary_key)

- create for *certification* only
- no optional comment. Since the semantics of the comment field are not well-defined, it has limited value for identification.

```bash
gpg --expert --full-generate-key
```

- select `ECC` (set your own capabilities)
- toggle capabilities so the primary key will only have the *certify* capability
- no expiration (read Gentoo Wiki)

After generating the primary key, be sure to backup the revocation certificate.

At this point, only the primary `[C]ertify` (key signing key) key has been created,
typically `[S]igning` and `[E]ncryption` keys are created as sub-keys.

### 2. Generate sub keys

- [Gentoo Wiki](https://wiki.gentoo.org/wiki/GnuPG)

```bash
gpg --expert --edit-key $KEY_ID
gpg> addkey
gpg> ...
gpg> save
```

- generate separate subkeys for encryption and signing
- add expiration date

A subkey is a cryptographic key attached to a primary (master) key in GPG. The primary key (also called the master key)
is used to certify and manage subkeys, while subkeys can be used for encryption, signing, or authentication.

Subkeys allow you to separate responsibilities and reduce risk. Instead of using your primary key for everything, you generate subkeys for specific tasks.

### 3. Removing the secret primary key for safety

- [Gentoo Wiki](https://wiki.gentoo.org/wiki/GnuPG#Removing_the_secret_primary_key_for_safety)

### 4. Verify that only subkeys are present

```bash
gpg --list-secret-keys
```

- `sec` = primary secret key is present
- `sec#` = primary secret key is not present (only public part of the primary key is present)

## Create new sub key

If your encryption subkey expires and you want to create a new one, you’ll need to do so while ensuring that your primary key is accessible — since you need the primary key to create and manage subkeys.

Since your primary secret key is stored on a USB drive for safety, you'll need to import it back into your GPG keyring temporarily to generate a new subkey.

### 1. Temporarily import your primary key

```bash
gpg --import /path/to/secret.gpg
```

### 2. Add subkey your key

```bash
gpg --expert --edit-key $KEY_ID

gpg> addkey
gpg> ...
gpg> save
```

### 3. Export updated sub keys

```bash
gpg --output $SUBKEYS_GPG_FILE --armor --export-secret-subkeys $KEY_ID
```

### 4. Remove all secret keys (primary + subkeys)

```bash
gpg --delete-secret-keys $KEY_ID
```

### 5. Import back the subkey secret keys

```bash
gpg --import $SUBKEYS_GPG_FILE
```

Verify that only subkeys are present.

---

## Usage

```bash
gpg --expert --edit-key $KEY_ID
```

List sub keys:

```bash
gpg> list
```

Select key for additional operations:

```bash
gpg> key <index>
```

### Usage fields

When listing GPG keys, the `usage` field indicates the capabilities of the key:

- [C]ertify (create and sign other keys)
- [S]ign data
- [E]ncrypt data

## Expiration date

- [Selecting expiration dates and using subkeys](https://www.gnupg.org/gph/en/manual.html#AEN526)

It is almost always the case that you will not want the master key to expire.

As long as the expired subkey is associated with the master key, it can still be used for decrypting files that were encrypted with it, even though it’s expired for encryption purposes.

Once a GPG **secret key** has expired, you cannot directly renew or extend the expiration date.

The expiration date is set at the time of key creation, and once the key has passed its expiration date,
it is considered invalid for cryptographic operations.

## Encryption subkeys

In scenario with multiple encryption subkeys:

### Encrypting a new message

GPG will only use active (non-expired) encryption subkeys.
It will pick the most recent valid encryption subkey.


### Decrypting old messages

GPG can still use expired subkeys for decryption, as long as their secret parts are present.
So you can decrypt messages encrypted with expired subkey.

## Revoking key components

- [gnupg.org](https://www.gnupg.org/gph/en/manual.html#AEN305)

Deleting user IDs and subkeys on your own key, however, is not always wise since it complicates key distribution. By
default, when a user imports your updated public key it will be merged with the old copy of your public key on his ring
if it exists. The components from both keys are combined in the merge, and this effectively restores any components you
deleted. Consequently, for updating your own key it is better to revoke key components instead of deleting them.

## Change passphrase secret key password

- [cyberciti.biz](https://www.cyberciti.biz/faq/linux-unix-gpg-change-passphrase-command/)

## Questions

Do the sub keys share password with primary key?

*Yes* - by default, all subkeys are protected using the same passphrase as the primary key, because:
The passphrase protects the entire private keyring entry (which includes the primary key and all its subkeys).
When you unlock one (e.g. for decryption or signing), GnuPG unlocks access to the required subkey in memory, assuming you authenticated correctly.

GnuPG does not support setting different passphrases per subkey in its normal keyring-based setup. The whole key block is encrypted with one passphrase.

---

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

### User ID

A user ID should be created carefully since it cannot be edited after it is created.

### Revocation certificate

After your keypair is created you should immediately generate a revocation certificate for the primary public key using
the option `--gen-revoke`.

A revoked public key can still be used to verify signatures made by you in the past, but it cannot be used to encrypt
future messages to you. It also does not affect your ability to decrypt messages sent to you in the past if you still do
have access to the private key.

Since the certificate is short, you may wish to print a hardcopy of the certificate to store somewhere safe such as your
safe deposit box. The certificate should not be stored where others can access it since anybody can publish the
revocation certificate and render the corresponding public key useless.

## Validation

Once a public key is imported to your public keyring it should be validated. GnuPG uses a powerful and flexible trust
model that does not require you to personally validate each key you import.

A key is validated by verifying the key's fingerprint and then signing the key to certify it as a valid key. A key's
fingerprint is verified with the key's owner. After checking the fingerprint, you may sign the key to validate it.

Once signed you can check the key to list the signatures on it and see the signature that you have added. Every user ID
on the key will have one or more self-signatures as well as a signature for each user that has validated the key.

## Encrypting and decrypting documents

- [gnupg.org](https://www.gnupg.org/gph/en/manual/x110.html)

A public key may be thought of as an open safe. When a correspondent encrypts a document using a public key, that
document is put in the safe, the safe shut, and the combination lock spun several times.

The corresponding private key is the combination that can reopen the safe and retrieve the document. In other words,
only the person who holds the private key can recover a document encrypted using the associated public key.

To encrypt a document the option `--encrypt` is used. You must have the public keys of the intended recipients.

If you want to encrypt a message to Alice, you encrypt it using Alice's public key, and she decrypts it with her private
key. In particular, you cannot decrypt a document encrypted by you unless you included your own public key in the
recipient list.

## Symmetric encryption (passphrase only)

Documents may also be encrypted without using public-key cryptography. Instead, only a symmetric cipher is used to
encrypt the document. The key used to drive the symmetric cipher is derived from a passphrase supplied when the document
is encrypted, and for good security, it should not be the same passphrase that you use to protect your private key.

## Digital signature

- [gnupg.org](https://www.gnupg.org/gph/en/manual/x135.html)

A digital signature certifies and timestamps a document. A signature is created using the private key of the signer. The
signature is verified using the corresponding public key.

### Signed document

- [gnupg.org](https://www.gnupg.org/gph/en/manual/r606.html)

The command-line option `--sign` is used to make a digital signature. The document to sign is input, and the signed
document is output.

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

Both the document and detached signature are needed to verify the signature. The `--verify` option can be to check the
signature.
