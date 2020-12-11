# Pods

## Example 01 - 01-pod-definition.yml

```bash
# Creating pod
kubectl create -f 01-pod-definition.yml
```

```console
kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
myapp-pod   1/1     Running   1          33m
```
## Editing an existing POD
```bash
vim 01-pod-definition.yml

# If you don't have the yml filem, you could extract the definition to a file:
kubectl get pod myapp-pod -o yaml > 01-pod-definition.yml

kubectl edit pod myapp-pod 
```