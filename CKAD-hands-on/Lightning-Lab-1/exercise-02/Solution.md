### Solution

#### Persistet Volume
```bash
# Check pods
kubectl get pods
kubectl exec -it webapp-color -- sh

# Check Services
kubectl get svc

# Check pod webapp-color
kubectl exec -it webapp-color -- sh

# Check connectivity port 80
nc -z -v -w 1 secure-service 80

# Check polices
kubectl get netpol
Lightning-Lab-1

```