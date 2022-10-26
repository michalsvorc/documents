# Kernel

## Compile

1. Compile the kernel.
   ```console
   make -j12
   ```
2. Any external kernel modules, such as binary kernel modules, need to be rebuilt for each new kernel.
   ```console
   emerge --ask @module-rebuild
   ```
3. Install kernel modules.
   ```console
   make modules_install
   ```
4. Export kernel image to `/boot`. Verify that partition containing the boot records is mounted as `\boot`.
   ```console
   make install
   ```

## Upgrade

- [Gentoo Wiki](https://wiki.gentoo.org/wiki/Kernel/Upgrade)

1. Select new kernel sources with `eselect`.
   ```console
   eselect kernel list
   eselect kernel set <target>
   ```
2. Copy `.config` file from the old kernel sources.
3. `cd` to the new kernel sources and run `make oldconfig`.
4. Compile the kernel and install kernel modules (see the Update section).

## Manage EFI boot entries

- [Gentoo Wiki](https://wiki.gentoo.org/wiki/Efibootmgr#Usage)

List the current boot entries:

```console
efibootmgr -v
```

## Update configuration

```console
make menuconfig
```

## Troubleshooting

- [Solving build problems](https://wiki.gentoo.org/wiki/Kernel/Upgrade#Solving_build_problems)

Always back up `.config`.

Pointing to old dependencies, e.g. previous version of GCC:

```console
make clean
make prepare
```
