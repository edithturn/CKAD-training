## **Problem**

Create a pod called time-check in the dvl1987 namespace.
This pod should run a container called time-check that uses the busybox image.
Create a config map called time-config with the data TIME_FREQ=10 in the same namespace.
The time-check container should run the command: while true; do date; sleep $TIME_FREQ;done 
and write the result to the location /opt/time/time-check.log.
The path /opt/time on the pod should mount a volume that lasts the lifetime of this pod.


## Solution

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