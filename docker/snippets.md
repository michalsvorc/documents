# Docker snippets

## Show disk usage

```shell
docker system df
```

## Clear docker cache

```shell
docker buildx prune
```

## Run one-time command inside container as root

```shell
docker exec -u 0 -it <container-id> <command>
```

### Chown a file

```shell
docker exec -u 0 -it <container-id> chown <user>:<group> <filepath>
```
