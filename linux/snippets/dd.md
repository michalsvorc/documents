# dd

- [Arch Wiki](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_basic_command_line_utilities)

```console
# dd bs=4M if=path/to/archlinux-version-x86_64.iso of=/dev/sdx conv=fsync oflag=direct status=progress
```
