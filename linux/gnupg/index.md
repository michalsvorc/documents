# GnuPG

- [Guides | gnupg.org](https://www.gnupg.org/documentation/guides.html)
- [FAQ | gnupg.org](https://www.gnupg.org/faq/gnupg-faq.html#glossary)
- [Public keys | gnupg.org](https://www.gnupg.org/gph/en/manual/x56.html)
- [GnuPG | gentoo.org](https://wiki.gentoo.org/wiki/GnuPG)
- [GnuPG | archlinux.org](https://wiki.archlinux.org/title/GnuPG)

## Usage

### Encrypt and sign file

```bash
gpg --encrypt --sign --recipient $RECIPIENT_KEY_ID file.ext
```

The signing key used is determined by:
- The `default-key` setting in your GnuPG configuration file (~/.gnupg/gpg.conf), if present.
- Otherwise, GnuPG selects the first suitable secret key it finds (one capable of signing).
- To explicitly specify the signing key, use the `--local-user $SIGNING_KEY_ID` option.

### Edit key

```bash
gpg --expert --edit-key $KEY_ID
```

List subkeys:

```bash
gpg> list
```

Select entry for additional operations:

```bash
gpg> key {index}
```

###  Ephemeral GnuPG directory

```bash
export GNUPGHOME=/path/to/dir
mkdir -p $GNUPGHOME
chmod 700 $GNUPGHOME
gpg --list-secret-keys
```

You can also execute only certain commands in ephemeral GnuPG directory.

```bash
gpg {command} --homedir /path/to/dir
```

Once finished, you can delete the directory. All GnuPG backend services that were started will detect this and shut down.

### Usage fields

- [C]ertify (create and sign other keys)
- [S]ign data
- [E]ncrypt data

## Change passphrase secret key password

- [cyberciti.biz](https://www.cyberciti.biz/faq/linux-unix-gpg-change-passphrase-command/)

## SSH

Wiki suggests possibility to manage SSH keys with GPG agent to have unified key management.

Skipped bc. it does not allow splitting to multiple SSH keys.

## FAQ

### Do the subkeys share password with primary key?

*Yes* - by default, all subkeys are protected using the same passphrase as the primary key, because:
The passphrase protects the entire private keyring entry (which includes the primary key and all its subkeys).
When you unlock one (e.g. for decryption or signing), GnuPG unlocks access to the required subkey in memory, assuming you authenticated correctly.

GnuPG does not support setting different passphrases per subkey in its normal keyring-based setup. The whole key block is encrypted with one passphrase.

### Trust level is unknown after import in ephemeral GNUPGHOME.

This behavior is expected. In GnuPG, trust is a local, per-keyring setting. GnuPG does not store the trust database
(`trustdb.gpg`) information within the exported private key file.

You can re-set the trust level manually in each new ephemeral GnuPG home directory. However, this is NOT necessary when
only generating new subkey and exporting it, as long as you will import that key into your main GnuPG keyring and set
the appropriate trust level there.
