# GnuPG: AEAD

- [Documentation | gnupg.org](https://www.gnupg.org/documentation/manuals/gnupg/OpenPGP-Options.html)
- [Gentoo discussion](https://bugs.gentoo.org/926186)
- [Archlinux discussion](https://wiki.archlinux.org/title/GnuPG#Disable_unsupported_AEAD_mechanism)
- [Stackexchange discussion](https://security.stackexchange.com/questions/275883/should-one-really-disable-aead-for-recent-gnupg-created-pgp-keys)

## Description

AEAD (Authenticated Encryption with Associated Data) is an encryption construction that provides confidentiality and
integrity simultaneously while allowing additional non‑encrypted data (associated data) to be authenticated.

In the OpenPGP ecosystem AEAD support has remained experimental and is not part of a finalized OpenPGP standard;
using AEAD changes message formats and requires both sender and recipient implementations to agree on the mode, which reduces interoperability.

For that reason many distributions disable or strip AEAD from packaged GnuPG builds, and hardware tokens such as YubiKey 5 (their OpenPGP
applet/firmware) do not implement AEAD.

Do not rely on AEAD when cross‑platform or hardware‑backed compatibility is required.
