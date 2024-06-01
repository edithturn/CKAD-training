# Kuberentes Security

The securityContext field in a Kubernetes Pod configuration is used to define privilege and access control settings for a Pod or Container.

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

- Here: The User ID defined in the securityContext of the container overrrides the User ID in ther POD
  the user which the pod is created is the 1002

```yaml
controlplane $ cat multi-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: multi-pod
spec:
  securityContext:
    runAsUser: 1001
  containers:
  -  image: ubuntu
     name: web
     command: ["sleep", "5000"]
     securityContext:
      runAsUser: 1002

  -  image: ubuntu
     name: sidecar
     command: ["sleep", "5000"]
```

## Example with Security Context as SYS_TIME capability

```yaml
apiVersion: v1
kind: Pod
spec:
  securityContext:
    runAsUser: 0
  containers:
    - command:
        - sleep
        - "4800"
      image: ubuntu
      imagePullPolicy: Always
      name: ubuntu
      resources: {}
      securityContext:
        capabilities:
          add: ["SYS_TIME"]
```

- Note:
  Capabilities are only supported at the container level and not at the POD level
