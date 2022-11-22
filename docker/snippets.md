# Docker snippets

## Run one-time command inside container as root

```console
docker exec -u 0 -it <container-id> <command>
```

Chown a file:

```console
docker exec -u 0 -it <container-id> chown <user>:<group> <filepath>
```
