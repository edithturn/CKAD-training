### Solution

**Check if the pod have connectivity with the service**

```bash
# Creating the pod
kubectl run time-check --image=busybox --dry-run -o yaml > pod.yaml
# Then edit the yaml to add extra configuration
```

```yaml

```

```bash
# Creating the pod with config map
kubectl apply -f pod.ymal

# Checking if the environment is created
kubectl -n dv1987 exec time-check env | grep time
```