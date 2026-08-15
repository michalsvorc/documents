# GnuPG: Concepts

## Keys and keypairs

- Symmetric cipher: uses the same secret key for encryption and decryption (used by passphrase-only encryption).
- Asymmetric (public-key) system: each user has a private key and a public key. The public key is shared; the private key is kept secret.

An OpenPGP certificate typically contains:
- A primary keypair: the certification authority for the certificate. Its private component creates self-signatures over user IDs, subkey-binding signatures, and revocations.
- Zero or more subkeys: subordinate keypairs bound to the primary key by binding signatures. Their capabilities are normally limited to encryption, data signing, and/or authentication.

### Why two-level keys?

- The main key is the identity anchor and should be kept offline as much as possible.
- Subkeys can be replaced, given shorter expiration dates, and stored on hardware tokens (for example, a YubiKey). Compromise of a subkey does not compromise the primary key's certification authority, but it can expose ciphertext decryptable by that subkey or permit forged data signatures until relying parties receive and honor a revocation.

### Best practices

- Keep the primary (main) key offline in secure storage. A certification-only primary key is common in an offline-primary-key design.
- Create subkeys for encryption, signing, and authentication and use those for daily work.
- Rotate or replace subkeys when needed (expiry, suspected compromise, algorithm or policy changes). Keep the primary key solely for certification, binding, expiration updates, and revocation.

## Expiration dates

- Primary keys and subkeys can have expiration dates. Expiration is encoded in self-signatures or subkey-binding signatures, not in immutable key material.
- Changing a primary-key or subkey expiration requires access to the private primary/certification key. GnuPG creates an updated self-signature or binding signature.

### Recommendation

Use expirations intentionally: set shorter expirations for subkeys used daily and keep the main key long‑lived and offline. It is almost always the case that you will not want the main key to expire. Expiration limits the window in which compliant software will select a key for new operations, but it does not prevent an attacker who already copied a private key from using it against past ciphertexts or signatures.

References:
- [GnuPG: Selecting expiration dates and using subkeys](https://www.gnupg.org/gph/en/manual.html#AEN526)

## Key size

- Within one algorithm family, larger parameters generally increase the cost of generic attacks. Security strength is not comparable by raw parameter length across algorithm families.
- For most practical purposes, default key sizes are sufficient — it is usually cheaper for an attacker to compromise an endpoint than to brute force a modern key.
- Larger key sizes can increase operation time and signature size.
- You cannot change an existing key's size; to use a different key length you must generate a new key or add new subkeys with different parameters.

### Recommendation

Prefer the modern algorithm choices provided by your installed GnuPG (many recent releases use ed25519/curve25519 or ed25519/cv25519 as the "future default"). When discussing "longer" keys note that comparisons are meaningful within an algorithm family (e.g., RSA). Do not directly compare RSA sizes to ECC curve names; they are different constructions with different security parameters.
- GnuPG defaults and available algorithms can change between releases; consult your installed `gpg --version` output and the local documentation for the definitive defaults on your system.

## User ID

- A User ID (UID) is an immutable OpenPGP packet, conventionally formatted as a name, optional comment, and email address, bound to the primary key by self-signatures and third-party certifications.
- A distributed UID cannot be edited or reliably deleted. Add a replacement UID and revoke the obsolete one; previously distributed copies may retain both packets.
- Choose UIDs carefully, and include an email/identifier you control.

References:
- [GnuPG: How to Specify a User Id](https://www.gnupg.org/documentation/manuals/gnupg/Specify-a-User-ID.html)

## Revocation certificate

- A revocation certificate is a signed revocation statement that, when published/imported by others, indicates that the key should be treated as revoked. GnuPG and other OpenPGP implementations will show a key as revoked once they see the revocation.
- Store the revocation certificate in an offline, secure place (safe, safe-deposit box, encrypted offline backup). Do not leave it where others can access it — anyone who obtains it can publish it and render your public key unusable.
- Generate a revocation certificate immediately after creating your primary key and back it up offline.

References:
- [GnuPG: Generating and publishing revocations](https://www.gnupg.org/documentation/manuals/gnupg/OpenPGP-Key-Management.html)

### What revocation does and does not do

- Importing a revocation causes software to display the key as revoked; revocation communicates intent and updates the key state for relying parties.
- A revoked key still verifies past signatures — signatures remain cryptographically verifiable even after revocation.
- Revocation does not prevent an attacker who already has a copy of the private key from decrypting earlier ciphertexts or producing signatures; it only signals to others that the key should no longer be trusted for new use.
- The private primary key can revoke subkeys and create updated expiration self-signatures or binding signatures. The pre-generated primary-key revocation certificate is primarily for the scenario where the private primary key is unavailable.

## Validation and trust model

GnuPG supports the Web of Trust (WoT) where key signatures indicate introductions or endorsements. In practice many users rely on direct fingerprint verification, TOFU, WKD/HTTPS, organizational keyservers, or explicit trust stores instead of an expansive WoT. Ownertrust (the local "ultimate" setting) is a local policy only and should normally be reserved for keys you control.

Practical advice
- Always verify fingerprints out-of-band before signing or otherwise trusting a key.
- Inspect who signed a key to understand the provenance, but remember that signatures alone do not prove identity unless you trust the signers as introducers.

References:
- [GnuPG: Trust values](https://www.gnupg.org/documentation/manuals/gnupg/Trust-Values.html)

## Encrypting and decrypting

- OpenPGP uses hybrid encryption: the implementation generates a fresh symmetric session key, encrypts the payload with it, and encrypts that session key to each recipient's public encryption key. Any holder of a corresponding private key can recover the session key and decrypt the payload.
- If you want to decrypt a message you previously encrypted to yourself, you must have included your own public key in the recipient list when encrypting, or you must be the only recipient.

References:
- [GnuPG: encryption and decryption commands](https://www.gnupg.org/documentation/manuals/gnupg/Operational-GPG-Commands.html)
- [OpenPGP: Hybrid encryption construction](https://www.rfc-editor.org/rfc/rfc9580.html#section-2.1)

### Symmetric encryption (passphrase-only)

- You can encrypt data with only a passphrase (no public keys) using symmetric encryption:
  `gpg --symmetric file.txt`
- GnuPG derives a key-encryption key from the passphrase using an OpenPGP S2K specifier; that key protects the per-message session key. Use a strong, unique passphrase that is not reused to protect a private key or another secret.

## Digital signatures

- A valid digital signature establishes integrity of the signed byte stream and demonstrates that the signing private key was used. A signature creation-time subpacket, when present, is signer-supplied metadata and can be backdated or postdated; it is not independent proof of signing time. Identity authentication requires a separately trusted binding between the signing key and the asserted identity.
- Create a signature with: `gpg --sign file.txt`

### Signed document formats

- Signed (binary): `--sign` produces an OpenPGP signed message containing the original literal-data packet and signature packet(s).
- Clearsigned: `--clearsign` produces a Cleartext Signature Framework message with a human-readable cleartext body and ASCII-armored signature. It applies dash escaping and canonical text processing, so it is not a byte-preserving format; prefer detached signatures when exact bytes matter.
- Detached signature: `--detach-sig` produces a separate signature file so the document remains untouched; verification needs both the document and the signature.

References:
- [GnuPG: Signature commands and verification caveats](https://www.gnupg.org/documentation/manuals/gnupg/Operational-GPG-Commands.html)
- [OpenGPG: Cleartext Signature Framework](https://www.rfc-editor.org/rfc/rfc9580.html#section-7)

## Quick practical checklist

- After generating a keypair:
  - Generate and securely store a revocation certificate.
  - Add appropriate expiration dates (shorter for subkeys).
  - Export and publish your public key where appropriate (direct sharing, WKD, or a keyserver). Be aware that keyserver publication is effectively permanent and may expose UIDs/email addresses — prefer direct sharing or WKD when privacy or the ability to remove data matters.
- For daily use:
  - Use subkeys for encryption/signing.
  - Keep the main key offline.
  - Replace subkeys on expiry, compromise, or an algorithm/policy transition; publish the updated certificate through the same discovery channels recipients use.
- For sharing/trusting:
  - Verify fingerprints out-of-band before signing others’ keys.

## References

- [GnuPG: Manual](https://www.gnupg.org/documentation/manuals/gnupg)
- [OpenPGP: RFC 9580](https://www.rfc-editor.org/rfc/rfc9580.html)
