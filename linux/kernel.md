# Kernel

## Source code location

```console
$ cd /usr/src/linux
```

## Configure kernel

```console
$ make menuconfig
```

## Compile kernel

```
$ make -j12
$ make modules_install
```

## Export to /boot

Verify that partition containing the boot records is mounted as `\boot`.

Export compiled kernel files to `/boot`:

```console
make install
```

## Troubleshooting

Pointing to old dependencies, e.g. previous version of GCC:

```console
$ make clean
$ make prepare
```
