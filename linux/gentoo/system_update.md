# Gentoo system update

## Portage

- [Portage Handbook - Gentoo Wiki](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Portage)
- [Portage - Gentoo Wiki](https://wiki.gentoo.org/wiki/Portage)
- [dispatch-conf - Gentoo Wiki](https://wiki.gentoo.org/wiki/Dispatch-conf)
- [Satisfying REQUIRED_USE conditions - Gentoo Wiki](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE#Satisfying_REQUIRED_USE_conditions)
- [Verify distfiles - Gentoo Wiki](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Features#Verify_distfiles)

Don't use Layman: [PSA: stop using Layman - reddit](https://www.reddit.com/r/Gentoo/comments/lxnktm/psa_stop_using_layman/)

## Process

### 1. Sync repositories

```console
$ emaint -a sync
```

### 2. Update packages

#### 2.1 Perform a dry run

```console
$ emerge -uvDNp \
    --with-bdeps=y \
    @world
```

Options:

- `--update, -u`
- `--verbose, -v`
- `--deep, -D`
- `--newuse, -N`
- `--pretend, -p`

Additional options:

- `--changed-use, -U`: add when the USE flags changed

#### 2.2 Perform an actual update

Remove the `-p` option. When preparing for large update, resize portage tmpfs.

```console
$ mount -o remount,size=N /var/tmp/portage
```

#### 2.3 Preserved rebuild

If prompted, upgrade any packages that remained built against old versions of libraries.

```console
$ emerge -av @preserved-rebuild
```

### 3. Remove obsolete and orphaned packages

```console
$ emerge -a --depclean
```

### 4. Merge configuration files

```console
$ dispatch-conf
```

## Optional

Verify changed dependencies

```console
$ emerge @changed-deps
```

Scan libraries for missing shared dependencies and re-merge any broken dependencies. Use in case of problems.

```console
revdep-rebuild -i
```

## NVIDIA drivers

Every time a kernel is built, it is necessary to reinstall the NVIDIA kernel modules.

```console
emerge @module-rebuild
```
