## **Problem**
We have deployed a few pods in this cluster in various namespaces. 
Inspect them and identify the pod which is not in a Ready state.
Troubleshoot and fix the issue.
Next, add a check to restart the container on the same pod if the command ls /var/www/html/file_check fails. 
This check should start after a delay of 10 seconds and run every 60 seconds.
You may delete and recreate the object. Ignore the warnings from the probe.

## **Solution**

Identify the pod that doesn't have a ready state

```bash
# Check the pod in state 0/1 in all namespaces
kubectl get pods --all-namespaces | grep 0
# Get the file definition of that pod
kubectl -n dev1401 get pod nginx1401 -o yaml > pod.yaml
```
```bash
# The probles is because readinesProbe is checking another port.

# Change the port of the readinessProbe with the same of the containerPort, edit the pod
vim pod.yaml 
# Now add a Liveness Probe in the Pod
```
```yaml
livenessProbe:
  exec:
    command:
      - ls
      - /var/ww/html/file_check
  initialDelaySeconds: 10
  periodSeconds: 60
```


```bash
# Delete the previous Pod created:
kubectl -n dev1401 delete pod nginx1401
# Create the new Pod
kubectl create -f pod.yaml
# Now the pod should be working
kubectl -n dev1401 get pods
# Check the livenessProbe
kubebctl -n dv1401 describe pod nginx1401 
```
