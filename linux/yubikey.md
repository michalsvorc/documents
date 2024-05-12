# Yubikey

- [Arch Wiki](https://wiki.archlinux.org/title/YubiKey)

Requirements:

- [PCSC](https://pcsclite.apdu.fr/): Middleware to access a smart card using SCard API (PC/SC).

Clients:

- [YubiKey Manager CLI](https://developers.yubico.com/yubikey-manager/): Python library and command line tool for configuring a YubiKey. 
- [YubiKey Manager QT](https://developers.yubico.com/yubikey-manager-qt/): Cross-platform application for configuring any YubiKey over all USB interfaces.
- [Yubico Authenticator](https://www.yubico.com/products/yubico-authenticator/)

Other:

- [Software projects](https://developers.yubico.com/Software_Projects/) 

## Start

Make sure PCSC daemon is running.

```shell
ykman info
```

Read using the [YubiKey Manager CLI](https://docs.yubico.com/software/yubikey/tools/ykman/Using_the_ykman_CLI.html).

## New account

- [URI string format](https://docs.yubico.com/yesdk/users-manual/application-oath/uri-string-format.html)

```shell
ykman oath accounts uri 'otpauth://totp/<user>?secret=<secret>&issuer=<issuer>'
```

## OTP

Get the Base32 secret key from QR code.

```shell
ykman oath accounts --help
```


