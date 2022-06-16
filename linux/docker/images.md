# Docker images

## Alpine Linux

- [Package management](https://wiki.alpinelinux.org/wiki/Alpine_Linux_package_management)
- [--no-cache Vs. rm /var/cache/apk](https://stackoverflow.com/questions/49118579/alpine-dockerfile-advantages-of-no-cache-vs-rm-var-cache-apk)

## Ubuntu

### .deb packages

Use `gdebi` to install .deb package with correct dependencies:

```console
# apt install gdebi-core
# gdebi ./<package.deb>
```

### Install recommends

- `--install-recommends`: default in Ubuntu
- `--no-install-recommends`: when image size matters
