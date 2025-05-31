# dm-crypt

- [dm-crypt | archlinux.org](https://wiki.archlinux.org/title/Dm-crypt)
- [dm-crypt | gentoo.org](https://wiki.gentoo.org/wiki/Dm-crypt)
- [cryptsetup FAQ | gitlab.com](https://gitlab.com/cryptsetup/cryptsetup/-/wikis/FrequentlyAskedQuestions)

## Notes

TRIM functionality on encrypted SSD drives is disabled: [archlinux.org](https://wiki.archlinux.org/title/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD))

## Encrypt device (non-system)

### 1. Wipe device

- [dm-crypt wipe on an empty device or partition | Arch Wiki](https://wiki.archlinux.org/title/Dm-crypt/Drive_preparation#dm-crypt_wipe_on_an_empty_device_or_partition)

`cryptsetup open` creates a block device mapper over the entire `/dev/sdX`. Writing to the mapper overwrites everything, partition table and partitions will both be destroyed.

```bash
cryptsetup open \
  --type plain \
  --cipher aes-xts-plain64 \
  --key-size 256 \
  --sector-size 4096 \
  --key-file /dev/urandom \
  /dev/sdX \
  <mapped_name>

dd if=/dev/zero of=/dev/mapper/<mapped_name> status=progress bs=1M

cryptsetup close <mapped_name>
```


The operation should exit after it encounters: `dd: error writing '/dev/mapper/<mapped_name>': No space left on device`.
Use of `if=/dev/urandom` is not required as the encryption cipher is used for randomness.
Setting the cipher during the temporary `cryptsetup open --type plain` (for wiping) does not affect later execution of `cryptsetup luksFormat`.

---

### 2. Create LUKS container

- [Default formatting options | archlinux.org](https://wiki.archlinux.org/index.php/dm-crypt/Device_encryption#Encryption_options_with_dm-crypt)

```bash
cryptsetup luksFormat --type luks2 /dev/sdX
```

Unlike the name implies, it does not format the device, but sets up the LUKS device header and encrypts the master-key
with the desired cryptographic options.

### 3. Open the LUKS container

Map the container with the device mapper:

```bash
cryptsetup open /dev/sdX <mapped_name>
```

### 4. Create a file system

```bash
mkfs.ext4 /dev/mapper/<mapped_name>
```

## Verify LUKS setup


After the LUKS container is created, make sure you're using `LUKS2` with strong derivation function:

```bash
cryptsetup luksDump /dev/sdX
```

Important to note:
- `Version`: 2
- `PBKDF`: argon2id

## LUKS UUID

When you encrypt a device with LUKS using cryptsetup luksFormat, it generates a unique LUKS UUID, stored in the LUKS header.

```bash
cryptsetup luksUUID /dev/sdX
```

## Backup

- [cryptsetup FAQ | gitlab.com](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#6-backup-and-data-recovery)

### Sector image backup

**NOTE**: Don't mount `/dev/sdX` or its mapper while backing it up, it must be *unmounted* and *inactive*.

Backup device:

```bash
dd if=/dev/sdX of=/mnt/backup/backup.img bs=4M status=progress conv=sync,noerror
```

Verify the backup, should return empty output when everything is all right.

```bash
cmp -n $(blockdev --getsize64 /dev/sdX) /dev/sdX /mnt/backup/backup.img
```

The sector image is already encrypted, but cannot be compressed and contains all empty space.

A sector-image will contain the whole partition in encrypted form, for LUKS the LUKS header, the keys-slots and the data area.
Note that compression is ineffective for encrypted data, hence it does not make sense to use it.

### LUKS header backup

If anything damages the LUKS header or the key-stripe area then decrypting the LUKS device can become impossible.
While the dd command will back up the entire partition (including the LUKS header), it’s generally recommended to also explicitly back up the LUKS header separately.
This is a precaution in case you ever need to restore the LUKS header or recover the data without using the dd image.
LUKS header backup is considered potentially sensitive data and should be backed up securely.

Be aware, that if you do keep a LUKS header backup and subsequently revoke any of the keyslots, the old keys will still be usable to unlock the LUKS partition for those with an access to that header backup file.

To back up the LUKS header, use the following command:

```bash
cryptsetup luksHeaderBackup /dev/sdX1 --header-backup-file /mnt/backup/luks-header.img
```

## Restore

The size of the target device should be equal or larger than the backup image.

Write the backup image onto the new device:

```bash
dd if=/mnt/backup/sdx-backup.img of=/dev/sdX bs=4M status=progress conv=sync,noerror
sync
```

Verify that LUKS headers are present on the new device:

```bash
cryptsetup -v isLuks /dev/sdX
```

## FAQ

### Can I resize a dm-crypt or LUKS container? [YES*]

- [cryptsetup FAQ | gitlab.com](https://gitlab.com/cryptsetup/cryptsetup/-/wikis/FrequentlyAskedQuestions#2-setup)

Yes, it is possible. Note that LUKS2 can use specified data-area sizes as a non-standard case and that these
may cause issues when resizing a LUKS2 container if set to a specific value.

Whether you should do this is a different question.
Personally I recommend backup, recreation of the dm-crypt or LUKS container with new size, recreation of the filesystem and restore.
