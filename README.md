# k8s-for-developers

## Kubectl

```bash
kubectl run hello-minikube
kubectl cluster-info
kubectl get nodes
```
## Namespaces
```bash
kubectl get namespaces
kubectl get pods --all-namespaces
```
## Yaml

### Requiered fields:
* apiVersion
* kind
* metadata
* spec

**pod-definition.yml**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels: 
  	app: my-frontend-app
  	type: front-end
spec:
 containers:
    - name: nginx-container
      image: nginx
```
## Pods
```bash
kubectl run nginx --image nginx
kubectl get pods

# More details about pods
kubectl get pods -o wide
kubectl  describe pod basicpod
```
```bash
# Creating pods based in yml files
kubectl create -f my-app.yaml
kubectl apply -f my-app.yaml
```
## Replication Controller | Replica Set 

The major difference between replication controller and replica set. 
is **selector**
"Selector" is requeired in replica set.
*ReplicaSet is the new recommended way fro scaling*

```bash
# Replication Controller
kubectl create -f rc-definition.yaml
kubectl get replicationcontroller
kuebectl get pods
```

```bash
# Replica Set
kubectl create -f rc-definition.yaml
kubectl get replicationcontroller
kuebectl get pods

# Also delete all the pods into this replicaset
kubectl delete replicaset myapp-replicaset
kubectl replace -f replicaset-definitionyml
kubectl scale -replicas=6 -f replicaset-definition.yml
```

## Basic Commands
```bash
kubectl api-resources
kubectl create -f basic.yaml
kubectl get pod
kubectl  describe pod basicpod

```

### Expose the port to the cluster
```bash
# Adding type NodePort in the service
* kubectl delete basicpod ; kubectl create -f basic.yaml
* kubectl create deployment firstpod --imagee=nginx
* kubectl get deployment, pod
* kubectl get namespaces
* kubectl get pod -n kube-system
* kubectl get pod -n default

# View resources in all namespaces at once. 
* kubbectl get pod --all-namespaces
* kubectl get deploy, rs, po, svc,ep

# Delete the top-level controller
kubectl delete deployment firstpod
```

### Build using a local Docker Registry

```bash
* kubectl create deployment <Deploy-Name> --image=<repo>/<app-name>:<version>
* kubectl create deployment time-date --image=10.110.186.162:5000/simpleapp:v2.2

# Iteractive shell:
* kubectl exec -i​t <Pod-Name> -- /bin/bash

# Logs
* kubectl logs test1
* kubectl -n kube-system logs etcd-ckad-1

# Become root using sudo
sudo -i
```

## Volumes
```bash
* kubectl create -f vol2.yaml
* kubectl get pv
```

### Converting a docke-compose file into yaml
sudo kompose convert -f docker-compose.yaml -o localregistry.yaml


### Dry run. Print the corresponding API objects without creating them.
```bash
kubectl create deployment drytry --image=nginx --dry-run=client -o yaml

k create deployment drytry -o yaml --image=nginx --dry-run=client > job1.yaml

sudo docker tag ubuntu:latest 10.110.186.162:5000/tagtest
sudo docker pull 10.110.186.162:5000/tagtest

kubectl create deployment try1 --image=10.110.186.162:5000/simpleapp
kubectl scale deployment try1 --replicas=6

```

### Deleting | Stopping 
```bash
kubectl delete --all pods --namespace=foo
kubectl delete --all deployments --namespace=foo
kubectl delete daemonsets,replicasets,services,deployments,pods,rc --all

```

kubectl apply -f https://k8s.io/examples/pods/probe/exec-liveness.yaml



## Liveness and Readiness Probes

There are three ways to implement Liveness and Readiness:

01. Running a command inside a container
02. Making an HTTP request against a container
03. pening a TCP socket against a container.


