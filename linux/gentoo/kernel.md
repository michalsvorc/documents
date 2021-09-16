# Kernel

## Update kernel

1. cd to source code location.

```console
$ cd /usr/src/linux
```

2. Configure the kernel.

```console
# make menuconfig
```

3. Compile the kernel.

```
# make -j12
```

4. Install kernel modules.

```
# make modules_install
```

5. Export to `/boot`.

Verify that partition containing the boot records is mounted as `\boot`.

```console
# make install
```

## [Kernel upgrade](https://wiki.gentoo.org/wiki/Kernel/Upgrade)

Select new kernel sources with `eselect`.

1. Copy `.config` from the old kernel sources.

2. cd to new kernel sources and use `make oldconfig` to update the `.config` file.

3. Compile the kernel.

4. Install kernel modules.

### Reinstalling external kernel modules

Examples of external modules: NVIDIA

The `modules_prepare` step is not required if building an entire kernel as this function is done as part of the standard process.

Any external kernel modules, such as binary kernel modules, need to be rebuilt for each new kernel.

```console
# emerge --ask @module-rebuild
# make modules_install
```

## [Manage EFI boot entries](https://wiki.gentoo.org/wiki/Efibootmgr#Usage)

List the current boot entries and `BootCurrent` value:

```console
# efibootmgr -v
```

## Troubleshooting

- [Solving build problems](https://wiki.gentoo.org/wiki/Kernel/Upgrade#Solving_build_problems)

Always back up `.config`.

Pointing to old dependencies, e.g. previous version of GCC:

```console
# make clean
# make prepare
```
