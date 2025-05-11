# GnuPG: Create new subkeys

If your encryption subkey expires and you want to create a new one, you’ll need to do so while ensuring that your primary key is accessible — since you need the primary key to create and manage subkeys.

Since your primary secret key is stored on a USB drive for safety, you'll need to import it back into your GPG keyring temporarily to generate a new subkey.

## 1. Temporarily import your primary key

```bash
gpg --import secret.gpg
```

## 2. Add subkey your key

```bash
gpg --expert --edit-key $KEY_ID

gpg> addkey
gpg> ...
gpg> save
```

## 3. Export updated subkeys

```bash
gpg --output subkeys.gpg --armor --export-secret-subkeys $KEY_ID
```

The GnuPG CLI does not provide a built-in way to export only a specific secret subkey directly via --export-secret-subkeys. The --export-secret-subkeys option exports all secret subkeys tied to a key ID.

## 4. Remove all secret keys (primary + subkeys)

*NOTE:* Works only when primary secret is present.

Allows granular secret key deletion, even when it says operation cancelled at the end when leaving a single key

```bash
gpg --delete-secret-keys $KEY_ID
```

## 5. Import back the subkey secret keys

```bash
gpg --import subkeys.gpg
```

Verify that only subkeys are present.
