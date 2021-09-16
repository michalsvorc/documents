# Gentoo installation

* [Handbook - Gentoo Wiki](https://wiki.gentoo.org/wiki/Handbook:Main_Page)
* [Security Handbook - Gentoo Wiki](https://wiki.gentoo.org/wiki/Security_Handbook/Full)
* [AppArmor - Gentoo Wiki](https://wiki.gentoo.org/wiki/AppArmor)

## Verify downloaded stage3 tarball

Import GPG key of Gentoo Linux Release Engineering team. Download digest.asc file and compare sha512 sum of stage tarball and asc file.

Follow the [Verifying the downloaded files](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Media#Verifying_the_downloaded_files) guide.

## Interrupting the installation process

Exit the chrooted guest environment.

```console
# exit
```

Unmount guest partitions from host image.

```console
# umount -l /mnt/gentoo/dev{/shm,/pts,}
# umount -R /mnt/gentoo
```

## Time

Set the BIOS clock to UTC. OS command `date` should show local time, while `date -u` should show UTC time.

Read: [Should I set my BIOS to local time or UTC? - superuser](https://superuser.com/questions/282551/should-i-set-my-bios-to-local-time-or-utc#:~:text=If%20multiple%20operating%20systems%20are,and%20set%20it%20to%20UTC).

## /etc/portage/make.conf

Don't use the plus one rule, use the exact number of CPUs.

Read: [MAKEOPTS - Gentoo Wiki](https://wiki.gentoo.org/wiki/MAKEOPTS)

## fstab

* [Fstab - Gentoo Wiki](https://wiki.gentoo.org/wiki/Fstab)

Set noauto on /boot: [Why is /boot 'noauto' in fstab? - Gentoo forums](https://forums.gentoo.org/viewtopic-t-157822-start-0.html)

## EFI stub boot

* [EFI Stub - Gentoo Wiki](https://wiki.gentoo.org/wiki/EFI_Stub)
* [EFI System Partition - Gentoo Wiki](https://wiki.gentoo.org/wiki/EFI_System_Partition)
* [Efibootmgr - Gentoo Wiki](https://wiki.gentoo.org/wiki/Efibootmgr)

## Microcode

* [Microcode - Gentoo Wiki](https://wiki.gentoo.org/wiki/Microcode)

### Intel

* [Intel microcode - Gentoo Wiki](https://wiki.gentoo.org/wiki/Intel_microcode)

Use the new method without initram-fs/disk (efistub compatible) section.

## OpenRC

* [OpenRC - Gentoo Wiki](https://wiki.gentoo.org/wiki/OpenRC)
* [Initscripts - Gentoo Wiki](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Initscripts)

Verify the service runlevel:

```console
rc-update -v show
```

Execute scripts during boot or shutdown: [/etc/local.d - Gentoo Wiki](https://wiki.gentoo.org/wiki//etc/local.d)

## X server

Read requirements for your DE.

Install session tracker: [Elogind - Gentoo Wiki](https://wiki.gentoo.org/wiki/Elogind)

Read Xorg and select your video card: [Xorg Guide - Gentoo Wiki](https://wiki.gentoo.org/wiki/Xorg/Guide)

## ACPI

Don't install ACPI daemon. Keep ACPI support in kernel (default), as some modules (e.g. graphic cards) depend on it.

## Power buttons

### systemd

```sh
# /etc/systemd/logind.conf

HandlePowerKey=poweroff
HandleSuspendKey=ignore
HandleHibernateKey=ignore
HandleLidSwitch=ignore
```
