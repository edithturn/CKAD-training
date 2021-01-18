# Kuberentes Security

It is possible configure the security settings at a container level or at a pod level.

## Pod Level

```yaml
apiVerson: v1
kind: Pod
metadata:
    name: web-pod
spec:
    securityContext:
        runAsUser: 1000
    containers:
        - name: ubuntu
        image: ubuntu
        command: ["sleep", "3600"]
```

## Container Level
```yaml
apiVerson: v1
kind: Pod
metadata:
    name: web-pod
spec:
    containers:
        - name: ubuntu
        image: ubuntu
        command: ["sleep", "3600"]
        securityContext:
        runAsUser: 1000
```

