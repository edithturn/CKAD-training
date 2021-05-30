### Solution

**Check if the pod have connectivity with the service**

```bash
# First create the config map
kubectl -n dvl1987 create cm time-config --from-literal=TIME_FREQ=10

# Creating the pod
kubectl run time-check --image=busybox --dry-run -o yaml > pod.yaml
# Then edit the yaml to add extra configuration check the file: pod.yaml
```

```bash
# Creating the pod with config map
kubectl apply -f pod.ymal

# Checking if the environment is created
kubectl -n dv1987 exec time-check env | grep time

HOSTNAME=time-check

```