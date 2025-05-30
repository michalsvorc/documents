# GnuPG: Configuration

- [Configuration | gentoo.org](https://wiki.gentoo.org/wiki/GnuPG#Configuration)
- [Configuration | archlinux.org](https://wiki.archlinux.org/title/GnuPG)

## gpg.conf

```bash
# Default key for signing and certifying operations.
default-key <KEY_ID>

# Use the default key as default recipient for encryption operation.
default-recipient-self

# Assume that command line arguments are given as UTF8 strings.
utf8-strings

# Adjusts digest algorithm selection order, can be utilized to prefer stronger hash types when signing messages.
personal-digest-preferences SHA512 SHA384 SHA256

# Sets the preference list, used by setpref in the edit menu, can be utilized to prefer stronger methods.
default-preference-list SHA512 SHA384 SHA256 SHA224 AES256 AES192 AES CAST5 ZLIB BZIP2 ZIP Uncompressed

# Specifies the preferred cipher algorithms for encrypting messages and generating keys, in order of preference.
personal-cipher-preferences AES256 TWOFISH CAMELLIA256

# The digest algorithm that will be used when signing a key.
cert-digest-algo SHA512

# The cipher algorithm which will be used by default for symmetric encryption.
s2k-cipher-algo AES256

# The digest algorithm which will be used to mangle passphrases used for symmetric encryption.
s2k-digest-algo SHA512

# Output
## Print additional information during processing.
verbose
## List keys options.
keyid-format long
with-fingerprint
with-subkey-fingerprints
```

## gpg-agent.conf

```bash
pinentry-program /usr/bin/pinentry
no-grab
default-cache-ttl 1800
```
