# Xorg

## Screen tearing issues

- [Screen tearing](https://www.maketecheasier.com/get-rid-screen-tearing-linux/)

### Intel

```sh
# /etc/X11/xorg.conf.d/20-intel.conf

Section "Device"
    Identifier "Intel Graphics"
    Driver "intel"
    Option "TearFree" "true"
EndSection
```

### Nvidia

Primary display:

```sh
# /etc/modprobe.d/nvidia-drm-nomodeset.conf

options nvidia-drm modeset=1
```

Arch: sudo mkinitcpio -p linux
Ubuntu: sudo update-initramfs -u

External display: Force composition pipeline in advanced display settings in nvidia-settings.
