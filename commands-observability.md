# Observability\*\*

```bash
# Collect failed pods by namespace, searching for events where the Liveness probe failed
kubectl -n qa get events | grep -i 'Liveness probe failed'

# Check pods in all namespaces with READY status = 0 (not ready)
k get pod --all-namespaces | grep -i 0

# Check the Liveness status of the 'nginx' pod
kubectl describe pod nginx | grep -i liveness

# Check the Readiness status of the 'nginx' pod
kubectl describe pod nginx | grep -i readiness

# View error events in the cluster
kubectl get events | grep -i error

# Copy the 'passwd' file from the 'busybox' container to the local machine
kubectl cp busybox:etc/passwd ./passwd
```
