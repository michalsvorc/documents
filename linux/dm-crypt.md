# dm-crypt

- [Arch Wiki](https://wiki.archlinux.org/title/Dm-crypt)
- [Gentoo Wiki](https://wiki.gentoo.org/wiki/Dm-crypt)

## Encrypt drive

### 1. Secure erase (optional)

- [dm-crypt/Drive preparation - Arch Wiki](https://wiki.archlinux.org/index.php/Dm-crypt/Drive_preparation)

Use dm-crypt specific methods.

### 2. Set header

```console
$ cryptsetup luksFormat /dev/sd<x>
```

Unlike the name implies, it does not format the device, but sets up the LUKS device header and encrypts the master-key
with the desired cryptographic options. See default [formatting
options](https://wiki.archlinux.org/index.php/dm-crypt/Device_encryption#Encryption_options_with_dm-crypt) that are
used.

### 3. Open device

Select a name for /dev/mapper:

```console
$ cryptsetup open /dev/sd<x> <name>
```

### 4. Create a filesystem

In order to write encrypted data into the partition it must be accessed through the device mapped name. The first step
of access will typically be to create a filesystem.

```console
$ mkfs -t <ext4 | btrfs> /dev/mapper/<name>
```

### 5. Close the mapped device

```console
cryptsetup close /dev/mapper/<name>
```
