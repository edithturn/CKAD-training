# Readiness Probes and Liveness Probes

In Kubernetes, readiness probes and liveness probes are mechanisms used to monitor the health and status of containers.

For HTTP:

```yaml
readinessProbe:
  httpGet:
    path: /app/ready
    port: 8080
```

For TCP:

```yaml
readinessProbe:
  tcpSocket:
    port: 3306
```

For EXEC:

```yaml
readinessProbe:
  exec:
    command:
      - cat
      - /ls
```

Example Pod Definition with Readiness Probe:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
    - image: nginx
      name: example-container
      ports:
        - containerPort: 8080
      readinessProbe:
        httpGet:
          path: /api/ready
          port: 8080
        initialDelaySecond: 10 # If we know our application will take 10 sencond in start
        periodSeconds: 5 # How oftern to probe the readiness
        failureThreshold: 8 # More than 3 attemps
```

`initialDelaySeconds`: Specifies the number of seconds to wait before performing the first readiness probe after the container has started.
`periodSeconds`: Defines how often (in seconds) to perform the readiness probe.
`failureThreshold`: Indicates the number of consecutive failures required before marking the container as not ready.

## Liveness Probe

A liveness probe in Kubernetes is used to determine if a container is still running. If a liveness probe fails, Kubernetes will restart the container to try to recover it. This helps ensure that applications can self-heal and recover from failures automatically.

For HTTP:

```yaml
livenessProbe:
  httpGet:
    path: /app/ready
    port: 8080
```

For TCP:

```yaml
livenessProbe:
  tcpSocket:
    port: 3306
```

For EXEC:

```yaml
livenessProbe:
  exec:
    command:
      - cat
      - /ls
```

Example Pod Definition with Liveness Probe:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
    - image: nginx
      name: example-container
      ports:
        - containerPort: 8080
      livenessProbe:
        httpGet:
          path: /api/healthy
          port: 8080
         initialDelaySeconds: 10
        periodSeconds: 5
        failureThreshold: 3
```

## Adding Liveness and Readiness Probes

1. **Create a Deployment Imperatively**:

```bash
kubectl create deployment example-deployment --image=nginx
```

2. **Edit the Deployment to Add Probes:**

```bash
kubectl edit deployment example-deployment
```

Imperative commands in Kubernetes, such as `kubectl run` or `kubectl create`, do not directly support the configuration of liveness probes and readiness probes. These probes are typically configured in the YAML definition of a pod or deployment.

However, you can create a basic pod or deployment using imperative commands and then edit the configuration to add the probes.

### Example Steps:

1. **Create a Deployment Imperatively**:

   ```bash
   kubectl create deployment example-deployment --image=nginx
   ```

2. **Edit the Deployment to Add Probes**:

   ```bash
   kubectl edit deployment example-deployment
   ```

   This will open the deployment configuration in your default text editor. You can then add the liveness and readiness probes.

### Example YAML Configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: example
  template:
    metadata:
      labels:
        app: example
    spec:
      containers:
        - name: example-container
          image: nginx
          ports:
            - containerPort: 80
          livenessProbe:
            httpGet:
              path: /healthz
              port: 80
            initialDelaySeconds: 10
            periodSeconds: 5
          readinessProbe:
            httpGet:
              path: /ready
              port: 80
            initialDelaySeconds: 5
            periodSeconds: 10
```
