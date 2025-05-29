# GnuPG: Create new keys (primary and subkeys)

In this ning and authentication are handled by subkeys. This separation of responsibilities justifies storing the *secret part of the primary key* on a separate, offline device (e.g., a flash drive) for safekeeping. The primary key is only needed for tasks like generating or renewing subkeys, or signing other people's keys.

*NOTE:*
- The *public part* of your primary key remains on your system, while its *secret part* is securely stored on a flash drive.
- The *current encryption subkey* remains active and available on your system, allowing you to decrypt new messages. Optionally, it can be moved to a secure hardware device like a YubiKey for added protection, under assumption it is backed up as well.
- *Older encryption subkeys* have had their secret parts removed from your system and archived on the flash drive. To decrypt files encrypted with these older subkeys, you’ll need to temporarily import the relevant secrets.
- As encryption subkeys expire, new encryption subkeys are generated and added incrementally.

In scenario with multiple encryption subkeys:
- GPG will only use active (non-expired) encryption subkeys.
- It will pick the most recent valid encryption subkey.
- GPG can still use expired subkeys for decryption, as long as their secret parts are present. You can decrypt messages encrypted with expired subkey.

## 1. Generate new primary key

- [Primary key | gentoo.org](https://wiki.gentoo.org/wiki/GnuPG#Primary_key)

Created for *certification* only.

```bash
gpg --expert --full-generate-key
```

**Steps:**
- Select `ECC (set your own capabilities)`.
- Toggle capabilities so the primary key will only have the *certify* capability.
- Selects elliptic curve, Gentoo Wiki suggests `Curve 25519`.
- Select no expiration (see *Primary key* section in Gentoo Wiki).
- No comment needed. Since the semantics of the comment field are not well-defined, it has limited value for identification.
- Add a passphrase. Before hitting final `<OK>`, be prepared to provide random user interaction inputs (keyboard, mouse) for increased entropy.

After generating the primary key, be sure to backup the revocation certificate.

At this point, only the primary `[C]ertify` (signing key) should have been created.

Verify with `gpg --list-keys`.

## 2. Generate subkeys

- [Add an encryption key | gentoo.org](https://wiki.gentoo.org/wiki/GnuPG#Add_an_encryption_key)

```bash
gpg --expert --edit-key $KEY_ID
gpg> addkey
gpg> ...
gpg> save
```

- generate separate subkeys for encryption and signing
- add expiration date (1Y)

A subkey is a cryptographic key attached to a primary (master) key in GPG. The primary key (also called the master key)
is used to certify and manage subkeys, while subkeys can be used for encryption, signing, or authentication.

Subkeys allow you to separate responsibilities and reduce risk. Instead of using your primary key for everything, you generate subkeys for specific tasks.

## 3. Export and remove primary key

- [Removing the secret primary key for safety | gentoo.org](https://wiki.gentoo.org/wiki/GnuPG#Removing_the_secret_primary_key_for_safety)

1. Extract the secret primary key (should be stored on another device):

```bash
gpg --armor --output primary.gpg --export-secret-key $KEY_ID
```

2. Validate that the subkeys do not contain stubs (e.g. moved to smartcard)

```bash
gpg --keyid-format long --list-secret-keys $KEY_ID
```

Look for stub symbol: `ssb>`. The regular subkeys should be: `ssb`.


3. Extract the secret subkeys:

```bash
gpg --armor --output subkeys.gpg --export-secret-subkeys $KEY_ID
```

4. Remove all secret keys (primary and subkeys):

```bash
gpg --delete-secret-keys $KEY_ID
```

5. Import the extracted secret subkeys (without the primary secret):

```bash
gpg --import subkeys.gpg
```

6. Verify that the primary secret key is not present:

```bash
gpg --list-secret-keys $KEY_ID
```

- `sec#`: primary secret key is not present (only public part of the primary key is present)
- `sec`: primary secret key is present
