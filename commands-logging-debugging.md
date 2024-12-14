# Logging and Debugging

```bash

# Run a busybox container that prints the date every 3 seconds
k run --image=busybox bbox -- sh -c 'while true; do date; sleep 3; done '

# View logs of the busybox container
kubectl logs busybox

# Follow the logs of the busybox container
kubectl logs busybox -f

# View logs from 'webapp-1' container and filter for 'USER5'
kubectl logs webapp-1 | grep USER5

# to select the containers
kubectl logs webapp-2 -c
kubectl logs webapp-2 -c simple-webapp
kubectl logs alta3pod | sudo tee ~/opt/answers/mypod.log

# See the error of a pod
kubectl get events | grep -i error

# Get logs from 'log-x' container in 'dev-pod', filter for warnings, and save them to /opt/logs.txt
kubectl dev-pod -c log-x | grep WARN > /opt/logs.txt

# To keep watching the logs
kubectl  logs bbox --follow

# Use describe
kubectl describe bbox

kubectl describe mydeploy

# See events for all resources in the cluster
kubectl get events

# Filter events for 'Schedule' keyword
kubectl get events | grep Schedule

# View logs of a pod created using kubectl run (e.g., 'bbox')
kubectl run --image=busybox bbox -- sh -c 'echo here; sleep 3600'

# Access the shell of a running pod ('bbox') interactively
kubectl exec -it bbox -- sh
ls
exit

# List all deployments across all namespaces
k get get deploy --all-namespaces

# List pods and services in the 'elastic-stack' namespace
kubectl -n elastic-stack get pod, svc

# Check more options for describing pods (e.g., volume mounts)
kubectl explain pods --recursive | less
/volumeMounts

# Monitor resource usage for nodes
kubectl top node

# Monitor resource usage for pods
kubectl top pod
```
