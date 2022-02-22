## Problems
Find pods running on any nodes having a memory limit configured and write the name of the pod having the highest memory limit configured to the file.
/opt/KUTR00402/KUTR00402.txt (which already exists)

## Solution
```bash
kubectl config use-contex k8s

# Inspect the nodes and look for the pod highest with the highest memory limit
kubectl get nodes
kubectl describe node k8s-master-0
kubectl describe node k8s-worker-1
kubectl describe node k8s-worker-2

# Print the names
kubectl get nodesecho coredns-0002 | sudo tee -a /opt/KUTR00402/KUTR00402.txt
```