# Kernel

## Upgrade

- [Gentoo Wiki](https://wiki.gentoo.org/wiki/Kernel/Upgrade)

1. Select new kernel sources with `eselect`.
   ```shell
   eselect kernel list
   eselect kernel set <target>
   ```
2.`cd` to the new kernel sources.
3. Copy `.config` file from the old kernel sources.
4. Run `make oldconfig`.
5. Compile the kernel and install kernel modules: [compile](#compile).

## Compile

1. Compile the kernel.
   ```shell
   make -j12
   ```
2. Any external kernel modules, such as binary kernel modules, need to be rebuilt for each new kernel.
   ```shell
   emerge --ask @module-rebuild
   ```
3. Install kernel modules.
   ```shell
   make modules_install
   ```
4. Export kernel image to `/boot`. Verify that partition containing the boot records is mounted as `\boot`.
   ```shell
   make install
   ```

## Update configuration

```shell
make menuconfig
```

## Manage EFI boot entries

- [Gentoo Wiki](https://wiki.gentoo.org/wiki/Efibootmgr#Usage)

List the current boot entries:

```shell
efibootmgr -v
```

## Troubleshooting

- [Solving build problems](https://wiki.gentoo.org/wiki/Kernel/Upgrade#Solving_build_problems)

Always back up `.config`.

Pointing to old dependencies, e.g. previous version of GCC:

```shell
make clean
make prepare
```
