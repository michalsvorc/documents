# GnuPG

- [Guides | gnupg.org](https://www.gnupg.org/documentation/guides.html)
- [FAQ | gnupg.org](https://www.gnupg.org/faq/gnupg-faq.html#glossary)
- [Public keys | gnupg.org](https://www.gnupg.org/gph/en/manual/x56.html)
- [GnuPG | gentoo.org](https://wiki.gentoo.org/wiki/GnuPG)
- [GnuPG | archlinux.org](https://wiki.archlinux.org/title/GnuPG)

## Set GNUPG directory

```bash
GNUPGHOME=/path/to/dir
```

## Usage

```bash
gpg --expert --edit-key $KEY_ID
```

List subkeys:

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

Once a GPG *secret key* has expired, you cannot directly renew or extend the expiration date.

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

Do the subkeys share password with primary key?

*Yes* - by default, all subkeys are protected using the same passphrase as the primary key, because:
The passphrase protects the entire private keyring entry (which includes the primary key and all its subkeys).
When you unlock one (e.g. for decryption or signing), GnuPG unlocks access to the required subkey in memory, assuming you authenticated correctly.

GnuPG does not support setting different passphrases per subkey in its normal keyring-based setup. The whole key block is encrypted with one passphrase.

## SSH

Wiki suggests possibility to manage SSH keys with GPG agent to have unified key management.

Skipped bc. it does not allow splitting to multiple SSH keys.
