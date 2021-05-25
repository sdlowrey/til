# Running an interactive shell in Docker

Handy when you want to explore or debug a container during development.

The availability of a shell depends on the base container.

The command to run an interactive shell is:

```shell
docker run --rm -i -t CONTAINER_NAME_OR_ID PATH_TO_SHELL
```

## Shells

/bin/ash : Alpine Linux