## Solution

Identify the pod that doesn't have ready state
```bash
kubectl get pods --all-namespaces | grep 0
kubectl -n dev1401 get pod nginx1401 -o yaml > pod.yaml

# Change the port of the readinessProbe with the containerPort
vim pod.yaml 
```

Now add a Liveness Probe in the Pod
```yaml
livenessProbe:
      exec:
        command:
        - ls
        - /var/ww/html/file_check
      initialDelaySeconds: 10
      periodSeconds: 60
```

Delete the previous Pod to create this one:
```bash
kubectl -n dev1401 delete pod nginx1401
kubectl create -f pod.yaml

# Now the pod should be working
kubectl -n dev1401 get pods
#Check 
kubebctl -n dv1401 describe pod nginx1401 
```
