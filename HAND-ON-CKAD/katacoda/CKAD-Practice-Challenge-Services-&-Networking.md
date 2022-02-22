# CKAD Practice Challenge: Services & Networking

## Imperative Commands

1. Create a pod named snip with image nginx and expose its port 80.

```bash
kubectl run snip --image=nginx --port:80
```

2. Create a service for pod snip on using ClusterIP type service with service name greef. Map service port 8080 to container port 80.
