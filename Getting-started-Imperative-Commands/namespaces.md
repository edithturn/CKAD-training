# **Namespaces**

## **Basic Commands**
```bash
# List all namespaces
kubectl get namespaces
kubectl get ns

# Create namespaces with a definition file
kubectl create -f namespace-dev.yml

# Create a namespace imperative commands
kubectl create namespace  default | kubectl get pods

# Count how many namespaces exists
kubectl get ns --no-headers | wc -l

# Check the current namespace
kubectl config view | grep namespace

# Listing all pod in all the namespaces
kubectl get pods --all-namespaces

# Listing all pod in a specific namespace
kubectl get pods --namespace=dev
kubectl -n dev get pods
```

```bash
# Create the pod in the default namespace
kubectl create -f pod-definition

# Create the pod in a specific namespace
kubectl create -f pod-definition.yml --namespace=dev

```
Add the namespace into the pod  yaml definition. 
```yml
metadata:
  name: myapp-pod
  namespace: dev
```

Create a namespace namespace-dev.yml
```yml
apiVersion: apps/v1
kind: Namespace
metadata:
    name: dev
```

```bash
# Set contex to the a namespace dev
kubectl config set-context $(kubectl config current-context) --namespace=dev

# Set contex to the a namespace default
kubectl config set-context $(kubectl config current-context) --namespace=default
```