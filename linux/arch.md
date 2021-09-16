# Arch Linux

## pacman

List all files installed by a package:

```console
$ pacman -Q | less
```

List orphans:

```console
$ pacman -Qdt
```

See dependency tree of installed package:

```console
$ pactree <package>
```

Remove a package along with its dependencies:

```console
$ pacman -Rns <package>
```

Removes targets that are not required by any other packages, use when removing a group:

```console
$ pacman -Ru <package>
```

Retrieve a list of the files installed by a particular package.:

```console
$ pacman -Ql <package>
```

check available package updates on your system:

```console
$ pacman -Syu
```

View detailed  package information before proceeding with the installation:

```console
$ pacman -Si <package>
```

List locally installed AUR packages:

```console
$ pacman -Qm
```

