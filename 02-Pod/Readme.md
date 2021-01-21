# Pods
Pods are a group of containers represented for deployable objects in Kubernetes. It could contain one or more containers.

![Pods](../img/pod/pod.png){:height="50%" width="50%"}

## Example 01 - 01-basic-pod-definition

```bash
# Listing pods
kubectl get pods
# More details about pods
kubectl get pods -o wide
kubectl  describe pod basicpod
```

```console
kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
myapp-pod   1/1     Running   1          33m
```

```bash
# Creating a pod from the kuberentes repository 
kubectl run nginx --image nginx
kubectl run nginx --image=nginx:alpine
# Creating pods based in yml files
kubectl create -f 01-pod-definition.yml
kubectl create -f my-app.yaml
kubectl apply -f my-app.yaml
```

## Editing an existing POD
```bash
vim 01-pod-definition.yml
# If you don't have the yml file, you could extract the definition to a file from a created Pod:
kubectl get pod myapp-pod -o yaml > 01-pod-definition.yml
kubectl edit pod myapp-pod 
```

## Deleting Pods
```bash
# Delete a pod, it will be created again by the deployment
kubectl delete pod [name-of-pod]
# Delete Deployment that manages the Pod, this will delete the Pod definitelly
kubectl delete deployment [name-of-deployment]
```
## More examples
```bash
kubectl apply -f /var/examples/webapp.yaml
```