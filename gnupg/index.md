# GnuPG

- [Guides | gnupg.org](https://www.gnupg.org/documentation/guides.html)
- [FAQ | gnupg.org](https://www.gnupg.org/faq/gnupg-faq.html#glossary)
- [Public keys | gnupg.org](https://www.gnupg.org/gph/en/manual/x56.html)
- [GnuPG | gentoo.org](https://wiki.gentoo.org/wiki/GnuPG)
- [GnuPG | archlinux.org](https://wiki.archlinux.org/title/GnuPG)

## Key fingerprint

For convenience while working with the commands, we can export the key id to an env variable:

```bash
export KEY_FPR='0123456789ABCDEF0123456789ABCDEF01234567'
```

Prefer full key fingerprints (40 hex chars) as key identifiers instead of short key IDs (8 hex chars); short IDs are susceptible to collisions and ambiguity.

## Encrypt and sign file

`$KEY_FPR` is the recipient GnuPG key (public key identifier) that will be used to encrypt the file; only the corresponding private key can decrypt it.

```bash
gpg --encrypt --sign --recipient $KEY_FPR file.txt
```
`--recipient`: selects the public key(s) used to encrypt the file.
  Only the holder(s) of the corresponding private key(s) will be able to decrypt.
`--sign`: signs the data with a secret key from your secret keyring.
  The signature is embedded alongside the encrypted data.


The signing key used is determined by:
- The `default-key` setting in your GnuPG configuration file (`$GNUPGHOME/gpg.conf`), if present.
- Otherwise, GnuPG selects the first suitable secret key it finds (one capable of signing).
- To explicitly specify the signing key, use the `--local-user $KEY_FPR` option.

## List keys

```bash
gpg --list-public-keys --keyid-format long --with-keygrip
gpg --list-secret-keys --keyid-format long --with-keygrip
```

You can also inspect a specific key to view its subkeys:

```bash
gpg --list-sercret-keys $KEY_FPR
```

If you have multiplpe primary keys, the grouping of primary key and subkeys is visual (groups are separated by an empty line).

## Key fields

```ini
sec   rsa4096/0123456789ABCDEF 2001-01-01 [C]
      Key fingerprint = 0123 4567 89AB CDEF 0123 4567 89ABC
      Keygrip = 11223344556677889900AABBCCDDEEFF00112233
```

- `rsa4096`: Algorithm + key size
- `0123456789ABCDEF`: Long key ID (16 hex chars = 64 bits), derived from the fingerprint (last 64 bits).
  Historically used for identification, not collision-resistant anymore.
- `2001-01-01`: Creation date
- `[?]`: Capabilities
- `Key fingerprint = 0123 4567 89AB CDEF 0123 4567 89ABC`: Full fingerprint (160 bits for SHA-1-based OpenPGP v4 keys).
  This is the real, canonical identifier, everything else is a shortcut. Use `--with-colons` to get the machine-readable
  version without whitespaces.
- `Keygrip = 11223344556677889900AABBCCDDEEFF00112233`: GnuPG-internal identifier, not part of OpenPGP.
  Used by gpg-agent to locate private keys on disk, such as `$GNUPGHOME/private-keys-v1.d/`.

### Capabilities

- [C]ertify - Create and sign other keys
  Grants the ability to issue certifications (signatures) that bind user IDs to a key or to sign someone else’s public key to vouch for its authenticity.
- [S]ign data - Sign files or messages
  Lets the key produce digital signatures over data (emails, files, commits) so recipients can verify the data’s integrity and the signer’s identity with the corresponding public key.
- [E]ncrypt data - Encrypt for the key owner / decrypt with the private key
  Means the public key can be used to encrypt data to the key owner (who uses the matching private key to decrypt).

NOTE: both Certify and Sign use digital signatures, but Certify signs key bindings (who owns which key) while Sign signs content.

### Primary sercret

- `sec`: secret primary key is present on the system
- `sec#`: secret primary key is not present (moved to a smartcard, only public part of the primary key is present)

### Subkeys

- `ssb`: secret subkey is present on the system
- `ssb>`: secret subkey is a **stub** (moved to a smartcard)

## Edit key

```bash
gpg --expert --edit-key $KEY_FPR
```

List subkeys:

```bash
gpg> list
```

Select entry for additional operations:

```bash
gpg> key {index}
```

## Change secret key passphrase

- [cyberciti.biz](https://www.cyberciti.biz/faq/linux-unix-gpg-change-passphrase-command/)

## SSH

Wiki suggests possibility to manage SSH keys with GPG agent to have unified key management.

Skipped bc. it does not allow splitting to multiple SSH keys.
