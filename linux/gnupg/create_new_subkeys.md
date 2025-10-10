# GnuPG: Create new subkeys

If your encryption subkey expires and you want to create a new one, you’ll need to do so while ensuring that your primary key is accessible — since you need the primary key to create and manage subkeys.

Since your primary secret key is stored on a USB drive for safety, you'll need to import it back into your GPG keyring temporarily to generate a new subkey.

## 1.  Set ephemeral GnuPG directory

```bash
export GNUPGHOME=/path/to/dir
mkdir -p -m 700 $GNUPGHOME
cp $HOME/.gnupg/{gpg.conf,gpg-agent.conf} $GNUPGHOME
gpg --list-secret-keys
```

## 2. Temporarily import your primary key

```bash
gpg --import primary.gpg
```

## 3. Temporarily import your subkeys

Necessary for exporting updated subkey set (old subkeys + new subkey) later.

```bash
gpg --import subkeys.gpg
```

## 4. Create new subkey

```bash
gpg --expert --edit-key $KEY_ID

gpg> addkey
gpg> ...
gpg> save
```

## 5. Export all subkeys (updated set)

```bash
gpg --armor --output subkeys.gpg --export-secret-subkeys $KEY_ID
```

The GnuPG CLI does not provide a built-in way to export only a specific secret subkey directly via --export-secret-subkeys. The --export-secret-subkeys option exports all secret subkeys tied to a key ID.

## 6. Set GnuPG directory to current keyring

```bash
export GNUPGHOME=$HOME/.gnupg
gpg --list-secret-keys
```

---

## 7. Import back subkeys

```bash
gpg --import subkeys.gpg
```

Verify that only subkeys are present. Primary key should have `sec#`.

```bash
gpg --list-secret-keys
```

## 8.A (Optional) Move new subkey to a smartcard

- [GnuPG Smart Card | gentoo.org](https://wiki.gentoo.org/wiki/GnuPG#Smart_Card)

## 8.B (Optional) Remove secret keys

*NOTE:* Works only when primary secret is present.
Remove unnecessary secret keys from the current keyring, leave only desired subkeys (currently in use).

*TEST:* If subkey was moved to a smartcard, this step is not necessary.

```bash
gpg --delete-secret-keys $KEY_ID
```
