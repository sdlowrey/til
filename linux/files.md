# Linux File Operations

## lsof

To find which process has a file open:

```shell
lsof -f -- /var/log/some-random.log
```

To see which files a process has open, first get the PID of the file. Then

```shell
lsof -p PID
```