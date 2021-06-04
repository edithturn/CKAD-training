## Problem

Create a redis deployment using the image redis:alpine with 1 replica and label app=redis. Expose it via a ClusterIP service called redis on port 6379. Create a new Ingress Type NetworkPolicy called redis-access which allows only the pods with label access=redis to access the deployment.

## Solution






## problem

Create a Pod called sega with two containers:

Container 1: Name tails with image busybox and command: sleep 3600.
Container 2: Name sonic with image nginx and Environment variable: NGINX_PORT with the value 8080.



## Solution

```bash
kubectl run sega --image=busybox --command sllep 3600 --dry-run=client = sega.yaml
vi sega.yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: sega
  name: sega
spec:
  containers:
  - command:
    - sleep
    - "3600"
    image: busybox
    name: tails
  - command:
    - sleep
    - "3600"
    image: nginx
    name: sonic
    env:
    - name: NGINX_PORT
      value: "8080"
```