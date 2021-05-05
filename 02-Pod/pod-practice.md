# Pods
### Example 01 - 01-basic-pod-definition

```bash
# Listing pods in the default namespace
kubectl get pods
# Listing pods in a different namespace
kubectl get pods --namespace=dev

# More details about all the Pods
kubectl get pods -o wide

# More details about a single Pod
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
kubectl run name --image=nginx
kubectl run redis --image redis123

# Creating pods based in yml files
kubectl create -f 01-pod-definition.yml
kubectl create -f my-app.yaml
kubectl apply -f my-app.yaml

# Creating pods in a specific namespace
kubectl create -f 01-pod-definition.yml --namespace=dev
kubectl run redis --image=redis --namespace=finance
```

**If we want to create a pod in diferent namespace defined in the yml file**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
  namespace: dev
  labels:
    app: myapp
    type: front-end
spec:
  containers:
  - name: nginx-container
    image: nginx
```

### Editing an existing Pod
```bash
vim 01-pod-definition.yml
# If you don't have the yml file, you could extract the definition to a file from a created Pod:
kubectl get pod myapp-pod -o yaml > 01-pod-definition.yml

# Create a dry run of the Pod, It will not create the pod, but we can use the yaml to redirect the yamls definition into a file called pod.yaml
kubectl run redis --image=redis123  --dry-run=client -o yaml > pod.yaml
# Editing the file, and save the changes.
vim pod.yaml
# Apply to create the pod
kubectl apply -f pod.yaml
kubectl get pod -n dev
```
**Example how to dry-run and edit the pod file**

```bash
kubectl run redis --image=redis --dry-run=client -o yaml > pod.yaml
# Editing the file, and save the changes, add namespace=dev
vi pod.yaml
kubectl apply -f pod.yaml
```
```bash
# Other ways to edit a file, edit will automatically apply the changes
kubectl edit pod myapp-pod
kubectl edit pod redis
```

### Deleting a Pod
```bash
# Delete a pod, it will be created again by the deployment
kubectl delete pod [name-of-pod]
# Delete Deployment that manages the Pod, this will delete the Pod definitelly
kubectl delete deployment [name-of-deployment]

# Deliting all pods in a namespace
kubectl delete --all pods --namespace=foo
```
### More examples
```bash
kubectl apply -f /var/examples/webapp.yaml
```