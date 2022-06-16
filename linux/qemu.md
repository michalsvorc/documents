# QEMU

- [Arch Wiki](https://wiki.archlinux.org/title/QEMU)
- [Overlay sotrage images - Arch Wiki](https://wiki.archlinux.org/title/QEMU#Overlay_storage_images)
- [Options - Gentoo Wiki](https://wiki.gentoo.org/wiki/QEMU/Options)
- [Linux Guest - Gentoo Wiki](https://wiki.gentoo.org/wiki/QEMU/Linux_guest)
- [9psetup - QUEMU Wiki](https://wiki.qemu.org/Documentation/9psetup#Example)

## Create new initial image

```console
$ qemu-img create -f qcow2 <name>.img <size>G
```

## Create new image overlay

```console
$ qemu-img create -f qcow2 -o backing_fmt=qcow2 -b <initial>.img <overlay>.img
```

## Pass USB device to guest

Lista available device:

```console
$ lsusb
```

Use the new hostdevice property of usb-host which is available since QEMU 5.1.0:

```console
-device qemu-xhci,id=xhci -device usb-host,hostdevice=/dev/bus/usb/00X/00Y
```