# GnuPG

- [Useful IT Policies](https://github.com/lfit/itpol/blob/master/protecting-code-integrity.md)

## RSA

- [Wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem))

RSA can be used for both asymmetric encryption and for digital signatures. An RSA key pair includes a private and a
public key.

The RSA private key is used to generate digital signatures, and the RSA public key is used to verify digital signatures.
The RSA public key is also used for key encryption of DES or AES DATA keys and the RSA private key for key recovery.

## Key pairs

- [Useful IT
  Policies](https://github.com/lfit/itpol/blob/master/protecting-code-integrity.md#understanding-the-certification-key)

By default, a master signing key and an encryption subkey are generated when you create a new keypair. This is
convenient, because the roles of the two keys are different, and you may therefore want the keys to have different
lifetimes.

- The master signing key is used to make digital signatures, and it also collects the signatures of others who have
  confirmed your identity.
- The encryption key is used only for decrypting encrypted documents sent to you.

Typically, a digital signature has a long lifetime, e.g., forever, and you also do not want to lose the signatures on
your key that you worked hard to collect. On the other hand, the encryption subkey may be changed periodically for extra
security, since if an encryption key is broken, the attacker can read all documents encrypted to that key both in the
future and from the past.

## Key roles

- E: encryption
- S: signing
- C: certification
- A: authentication

## Key Ids

Key IDs can be represented in three different forms:

- fingerprint, a full 40-character key identifier (111122223333444455556666AAAABBBBCCCCDDDD)
- long, last 16-characters of the fingerprint (AAAABBBBCCCCDDDD)
- short, last 8 characters of the fingerprint (CCCCDDDD)

## Create new key pair

- [Arch wiki](https://wiki.archlinux.org/title/GnuPG#Create_a_key_pair)
- [Gentoo wiki](https://wiki.gentoo.org/wiki/GnuPG#Creating_a_key)

```console
$ gpg --full-gen-key
```

- The default 'RSA and RSA'
- Use a keysize of the default 3072 value.
- Expiration date: 0 (never expire). Set expiration date for encryption subkey later, unless revoked (see Subkeys
  section).

After creating a key pair, backup your private key and revocation certificate to offline encrypted device.

### Backup revocation certificate

- [Arch wiki](https://wiki.archlinux.org/title/GnuPG#Backup_your_revocation_certificate)
- [Gentoo wiki](https://wiki.gentoo.org/wiki/GnuPG#Generating_a_revocation_certificate)
- [GnuPG manual](https://www.gnupg.org/gph/en/manual.html#REVOCATION)

Revocation certificates are automatically generated for newly generated keys. These are by default located in
~/.gnupg/openpgp-revocs.d/. 

The certificate should not be stored where others can access it since anybody can publish the revocation certificate and
render the corresponding public key useless.

### Backup your private key

- [Arch wiki](https://wiki.archlinux.org/title/GnuPG#Backup_your_private_key)

## Subkeys

It only makes sense to have one valid encryption subkey on a keyring. There is no additional security gained by having
two or more active subkeys. There may of course be any number of expired keys on a keyring so that documents encrypted
in the past may still be decrypted, but only one subkey needs to be active at any given time.

### Expiration date

- [Arch wiki](https://wiki.archlinux.org/title/GnuPG#Extending_expiration_date)
- [GPG manual](https://www.gnupg.org/gph/en/manual.html#AEN526)

It is almost always the case that you will not want the master key to expire. One reason for master key expiration might
be that if you lose control of the key and do not have a revocation certificate with which to revoke the key, having an
expiration date on the master key ensures that the key will eventually fall into disuse.

It is good practice to set an expiration date on your subkeys, so that if you lose access to the key (e.g. you forget
the passphrase) the key will not continue to be used indefinitely by others. 

```console
$ gpg --edit-key <user_id>
$ key <N> # select subkey by index N
$ expire
$ save
```

Alternatively, if you prefer to stop using subkeys entirely once they have expired, you can create new ones. Do this a few weeks in advance to allow others to update their keyring.

GPG key's expiration can also be extended at any time unless it's been revoked.

! Never delete your expired or revoked subkeys unless you have a good reason. Doing so will cause you to lose the ability to decrypt files encrypted with the old subkey. Please only delete expired or revoked keys from other users to clean your keyring.

### Exporting subkey

- [Arch wiki](https://wiki.archlinux.org/title/GnuPG#Exporting_subkey)

If you plan to use the same key across multiple devices, you may want to strip out your master key and only keep the bare minimum encryption subkey on less secure systems. 

## GPG agent

- [Arch wiki](https://wiki.archlinux.org/title/GnuPG#gpg-agent)
- [Gentoo wiki](https://wiki.gentoo.org/wiki/GnuPG#Using_a_GPG_agent)

Set GPG agent using Gentoo wiki.

## Additional notes

If a user has several email addresses they would like to use with the key, the user can run gpg `--edit-key <USER_ID>` then use the adduid command.
It will ask the user for the name, email, and comment of the second ID to be used.

## Pass

- [Arch wiki](https://wiki.archlinux.org/title/Pass)

To be able to use pass, set up GnuPG. The trust level of the key used for pass must be "ultimate".

Upon initialization of pass store, you provide GPG identity. Plaintext identity will be stored as.gpg-id. This tells pass which key to use for pass operations.

Passphrase for the private key will become passphrase for document encryption/decryption.

You can still decrypt passwords using expired encryption key.
