# Resources Request

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: my_app
    labels:
        name: my_app
spec:
    containers:
    - name: my_app
    image: my_app
    ports:
        - containerPort: 8080
    resources:
        request:
        memory: "1Gi"
        cpu: 1

```

## Adding limits to the container

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: my_app
    labels:
        name: my_app
spec:
    containers:
    - name: my_app
    image: my_app
    ports:
        - containerPort: 8080
    resources:
        request:
        memory: "1Gi"
        cpu: 1
    limits:
        memory: "2Gi"
        cpu: 2
```

