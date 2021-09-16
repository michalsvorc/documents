# Docker service

- [Arch wiki](https://wiki.archlinux.org/title/docker)
- [Gentoo wiki](https://wiki.gentoo.org/wiki/Docker#Compatibility_check)
- [Network Drivers](https://docs.docker.com/network/)
- [Storage Drivers](https://docs.docker.com/storage/storagedriver/select-storage-driver/)
- [User namespace isolation](https://wiki.archlinux.org/title/docker#User_namespace_isolation)

## System compatibility check

- Re-emerge `app-emulation/docker`. It prints compatibility flag info at the beginning of compilation.
- [Script](https://github.com/moby/moby/blob/master/contrib/check-config.sh)

## Kernel configuration

Ignore Gentoo wiki kernel section, read output of emerge `app-emulation/docker`.

When enabling flags, build modules where it is suggested by enabling (M) option as first selection.

Re-emerge `app-emulation/docker` after rebuilding and reloading the kernel.

## Configuration file

- [OpenRC](https://wiki.gentoo.org/wiki/Docker#OpenRC_2)
- [Options](https://docs.docker.com/engine/reference/commandline/dockerd/#/options)

Use `docker info` command to see docker settings.

## Permissions

To use Docker as a non-root user, add yourself to the 'docker' group:

```console
$ usermod -aG docker <user_name>
```

## Gentoo packages

Starting with docker 20.10.2, docker has been split into
two packages upstream, so Gentoo has followed suit.

* app-emulation/docker contains the daemon and
* app-emulation/docker-cli contains the docker command.

Docker currently installs docker-cli using the cli use flag.

This use flag is temporary, so you need to take the following actions:

1. First, disable the cli use flag for app-emulation/docker

2. Then, if you need docker-cli and docker on the same machine, run the following command:

```console
$ emerge --noreplace docker-cli
```

## Troubleshooting

### Test images

```console
$ docker run --rm hello-world
```

Networking:

```console
$ docker run --rm -p 8080:8080 --name nginx-test bitnami/nginx:latest
```

## Rootless containers

### WORKDIR command

WORKDIR command with non-existent directory argument creates directory as a root. Switch to non-system USER and use:

```docker
RUN mkdir "${HOME}/${work_dir}" 
```

You can then use WORKDIR to switch to a newly created directory with non-system permissions.

### Mount volumes

* [Add ability to mount volume as user other than root · Issue #2259 · moby/moby](https://github.com/moby/moby/issues/2259)

Solutions:

* [User namespace isolation](https://wiki.archlinux.org/title/docker#User_namespace_isolation)
* Recursive chown
