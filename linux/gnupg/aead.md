# GnuPG: AEAD

[Documentation | gnupg.org](https://www.gnupg.org/documentation/manuals/gnupg/OpenPGP-Options.html)
[Gentoo discussion](https://bugs.gentoo.org/926186)
[Archlinux discussion](https://wiki.archlinux.org/title/GnuPG#Disable_unsupported_AEAD_mechanism)
[Stackexchange discussion](https://security.stackexchange.com/questions/275883/should-one-really-disable-aead-for-recent-gnupg-created-pgp-keys)

## 250530

As of gpg (GnuPG) 2.4.7, AEAD is not standardized and YubiKey v5 does not support it. Major GNU/Linux distributions
strip the AEAD support in GnuPG packages.
