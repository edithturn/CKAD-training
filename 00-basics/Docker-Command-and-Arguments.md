## Commands and Arguments in Docker

```Dockerfile
FROM Ubuntu
CMD sleep 5
```


**Examples**
```bash
CMD command param1
CMD ["command", "param1"]
```

```bash
CMD sleep 5
CMD ["sleep", "5"]
```
```bash
docker run ubuntu-sleeper 10
```

```Dockerfile
FROM Ubuntu
ENTRYPOINT ["sleep"]
```

```Dockerfile
FROM Ubuntu
ENTRYPOINT ["sleep"]
CMD ["5"]
```

To send the command at startup, we use :
```bash
docker run --entrypoint sleep2.0 ubuntu-sleeper 10
```