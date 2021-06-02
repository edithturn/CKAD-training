## **Problem**

We have deployed a new pod called secure-pod and a service called secure-service. Incoming or Outgoing connections to this pod are not working.
Troubleshoot why this is happening.

Make sure that incoming connection from the pod webapp-color are successful.


Important: Don't delete any current objects deployed.

## **Solution**

**Check if the pod have connectivity with the service**
```bash
# Check pods
kubectl get pods
kubectl exec -it webapp-color -- sh

# Check Services, in which port is runnning the secure-service?
kubectl get svc # secure-service

# Check pod webapp-color
kubectl exec -it webapp-color -- sh

# Check connectivity port 80
nc -z -v -w 1 secure-service 80

# Example
For example, to scan for open ports in the range 20-80 you would use the following command:

nc -z -v 10.10.8.8 20 80

The -z option will tell nc to only scan for open ports, without sending any data to them and the -v option to provide more verbose information and -w for connections which cannot be established or are idle timeout after timeout seconds

# Check polices
kubectl get netpol
kubectl get pod --show-labels
# -> secure-pod  LABELS: run=secure-pod
```
**Creating the police**

```bash
kubectl apply -f netpol.yaml

# Check pod webapp-color again
kubectl exec -it webapp-color -- /bash/sh 
nc -v -z -w 1 10.10.8.8 20 80
# secure-service (10.10.8.8:80) open
```