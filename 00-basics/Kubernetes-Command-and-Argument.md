## Kubernetes Commands and Arguments

```bash
docker run --name ubuntu-sleeper ubuntu-sleeper
docker run --name ubuntu-sleper ubuntu-sleeper 10
```

### Example 01

The ENTRYPOINT in the Dockerfile is overridden by the command in the pod definition.

Since the entrypoint is overridden in the pod definition, the command that will be run is just --color green

```yaml
apiVersion: v1 
kind: Pod 
metadata:
  name: webapp-green
  labels:
      name: webapp-green 
spec:
  containers:
  - name: simple-webapp
    image: kodekloud/webapp-color
    command: ["--color","green"]
```

```Dockerfile
FROM python:3.6-alpine

RUN pip install flask

COPY . /opt/

EXPOSE 8080

WORKDIR /opt

ENTRYPOINT ["python", "app.py"]

CMD ["--color", "red"]
```

### Example 02: What command is run at container startup?

```Dockerfile
FROM python:3.6-alpine

RUN pip install flask

COPY . /opt/

EXPOSE 8080

WORKDIR /opt

ENTRYPOINT ["python", "app.py"]

CMD ["--color", "red"]
```

```yml
apiVersion: v1 
kind: Pod 
metadata:
  name: webapp-green
  labels:
      name: webapp-green 
spec:
  containers:
  - name: simple-webapp
    image: kodekloud/webapp-color
    command: ["python", "app.py"]
    args: ["--color", "pink"]
```

python aoo.py  --color pink