## **Readiness Probe**

The function of a Readiness is the ready condition of a Pod to the actual state of the application inside.

There are several ways to check if the application on the pod is ready

Pod deinition
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    ports:
      - containerPort: 8080
    readinessProbe:
        httpGet:
          path: /api/ready
          port: 8080
```

**httpGet**
```yaml
radinessProbe:
    httpGet:
        path: /api/ready
        port: 8080
    initialDelaySeconds: 10
    periodSeconds: 5
    failireThreshold: 8
```
**tcpSocket**
```yaml
radinessProbe:
    tcpSocket:
        port: 8080
```

**command**
```yaml
radinessProbe:
    exec:
        command:
            - cat
            - /app/is_ready
```

## **Liveness Probe**
Can be configured in the container to periodically test the application within the container is actualli healthy.

Pod deinition
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    ports:
      - containerPort: 8080
    livenessProbe:
        httpGet:
          path: /api/healthy
          port: 8080
```
**Http Test**
```yaml
livenessProbe:
    httpGet:
        path: /api/healthy
        port: 8080
```
**tcpSocket**
```yaml
livenessProbe:
    tcpSocket:
        port: 3306
```
**Exec command**
```yaml
livenessProbe:
    exec:
        command:
            - cat
            - /app/is_healthy
```

## Imperative command
```bash
# Generate the yaml file
kubectl create deploy livenessprobe --image busybox -o yaml --dry-run

# Generate the file in a yaml file
kubectl create deploy livenessprobe --image busybox -o yaml --dry-run > livenessprobe.yaml
```