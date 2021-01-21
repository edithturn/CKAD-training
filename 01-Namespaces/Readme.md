# Namespaces

## Basic Commands
```bash
kubectl get namespaces
kubectl get pods --all-namespaces
kubectl get pods --namespace=kube-system
```
```bash
# Create the pod in the default namespace
kubectl create -f pod-definition

# Create the pod in a specific namespace
kubectl create -f pod-definition.yml --namespace=dev
```
* Adding the name of the namespace into the yml file. 
```yml
metadata:
  name: myapp-pod
  namespace: dev
```
## Create a namespace namespace-dev.yml
```yml
apiVersion: apps/v1
kind: Namespace
metadata:
    name: dev
```
```bash
# Create namespaces with a namespace definition file
* kubectl create -f namespace-dev.yml

# Create a namespace without a yml file
* kubectl create namespace  default | kubectl get pods
* kubectl create namespace  dev | kubectl get pods --namespace=dev
* kubectl create namespace  prod | kubectl get pods --namespace=prod
```

## Switch to a specific namespace permanently
```bash
> kubectl get pods  
> kubectl get pods --namespace=dev 
> kubectl get pods --namespace=prod

# Switching namespace to dev
* kubectl config set-contex $(kubectl config 
current-context) --namespace=dev

> kubectl get pods 
> kubectl get pods --namespace=default 
> kubectl get pods --namespace=prod

# Switching namespace to prod
* kubectl config set-contex $(kubectl config 
current-context) --namespace=prod

> kubectl get pods --namespace=dev 
> kubectl get pods --namespace=default  
> kubectl get pods

# List all the pods in all the namespaces
> kubectl get pods --all-namespaces
```