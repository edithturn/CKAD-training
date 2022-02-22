## **Problem**
Create an nginx pod and load environment values from the above configmap envcfgmap and exec into the pod and verify the environment variables and delete the pod

```bash
# Create the yaml definiton for nginx pod
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > nginx-pod.yml

# Edit the yam to add a Config Map as a environment (configMapKeyRef) - see nginx-pod.yml 
vim nginx-pod.yaml

# Then create the pod
kubectl create -f nginx-pod.yaml

# Check if the variable from the Config Map is in the System environment
kubectl exec -it nginx -- env

```

## **Solution**
