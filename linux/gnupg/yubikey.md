# GnuPG: YubiKey

- [GnuPG Smart Card | gentoo.org](https://wiki.gentoo.org/wiki/GnuPG#Smart_Card)
- [YubiKey | gentoo.org](https://wiki.gentoo.org/wiki/YubiKey/GPG)
- [Setting PINs | gentoo.org](https://wiki.gentoo.org/wiki/YubiKey/GPG#Setting_PINs)

YubiKey implements the OpenPGP smart card specification, which has three slots:

- Signature (sig)
- Encryption (enc)
- Authentication (auth)

Each slot holds **only one private key**.

List card status:

```bash
gpg --card-status
```

Edit card interface:

```bash
gpg --card-edit
```

## Move secret key to card

- [Loading keys | gentoo.org](https://wiki.gentoo.org/wiki/YubiKey/GPG#Loading_Keys)

**IMPORTANT:**
- `keytocard` command deletes the associated secret key from the system, and overwrites what is in that slot on the YubiKey. Ensure keys have been backed up before using this.
- *Note*: the keys are 0-indexed.

```bash
gpg --expert --edit-key $KEY_ID
gpg> key <N\>
gpg> keytocard
gpg> >provide gpg passphrase
gpg> >provide smartcard admin PIN
gpg> save
```

## Import secret key moved to card from a backup

When the key was moved to card, the current keygrip references it as a stub. Even after deleting a subkey and
re-importing it from full subkey backup, GnuPG may retain subs or keygrips in internal files, databases or agent cache.

To fix this:

1. Kill the gpg agent

```bash
gpgconf --kill gpg-agent
```

2.A Quickfix to access moved subkey: set different `GNUPGHOME` and re-import from backup.

2.B Permafix:

*NOTE* Verify that you have valid backups before proceeding.

Get the keygrip of the subkey:

```bash
gpg --with-keygrip --list-secret-keys $KEY_ID
```

Remove the keygrip file from `$GNUPGHOME/private-keys-v1.d/<keygrip-id>.key`

Re-import from the backup.

## Force the YubiKey to be touched to use any of the loaded keys

- [Forcing presence detection for key usage](https://wiki.gentoo.org/wiki/YubiKey/GPG#Forcing_presence_detection_for_key_usage)

```bash
ykman openpgp keys set-touch <KEY> ON
```

Key values:
- `SIG`
- `DEC`
- `AUT`
- `ATT`
