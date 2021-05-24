# Kubernetes For Developers

<p align="center">
  <img width="500" height="350" src="img/k8s.png">
</p>


# `` REPOSITORY IN PROGRESS ... `` :carousel_horse: :raising_hand:  :tractor:

## Componentes
- API Server
- etcd
- kubelet
- Container Runtine
- Controller
- Scheduler

## Architecture
  A node is a machine physical or virtual, and node is a worker machine and that is where containers will be launched by Kubernetes.

## Key Kubernetes Features
* Service Discoverry/Load Balancing
* Storage Orchestration
* Automate Rollouts/Rollbacks
* Self-healing
* Secret and Configuration Management
* Horizontal Scaling

## Key Container Benefits
* Accelerate Developer Onboarding
* Eliminate App Conficts
* Environment Consistency
* Ship Software Faster

[Add : Source]

## Why we need kubernetes as a developers?


## Kubectl

```yaml
kubectl version
kubectl cluster-info
kubectl --help
kubectl get all
kubectl run [container-name] --image=[image-name]
kubectl port-forward [pod] [ports]
kubectl create [resource]
kubectl apply [resource]
kubectl get nodes
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

## Creating YAMLS

```bash
kubectl create deployment nginx --image=nginx --dry-run=client -o ymal > nginx-deployment.yaml
```

* [Pods](02-Pod/Readme.md)

* [Replication Controller](04-Replication-controller/Readme.md)

* [Deployments](03-Deployment/Readme.md)

* [Services](11-Services/Readme.md)

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
* kubectl create deployment firstpod --image=nginx
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


### Deleting | Stopping 
```bash
> kubectl delete --all pods --namespace=foo
> kubectl delete --all deployments --namespace=foo
> kubectl delete daemonsets,replicasets,services,deployments,pods,rc --all
```


## Secrets
```bash
* kubectl get secrets
* kubectl describe secret my-secret
* kubectl create secret generic db-secret --from-literal=DB_Host=sql1
--from-literal=DB_User=root
--from-literal=DB_Password=password123

```


## Liveness and Readiness Probes

There are three ways to implement Liveness and Readiness:

01. Running a command inside a container
02. Making an HTTP request against a container
03. pening a TCP socket against a container.

```bash
kubectl apply -f https://k8s.io/examples/pods/probe/exec-liveness.yaml
```

## --dry-run
```bash
kubectl [command] [TYPE] [NAME] -o <output_format>
kubectl create --dry-run=client -o yaml
kubectl create namespace test-123 --dry-run -o yml
<output_format>
* -o json
* -o name
* -o wide
* -o yaml
```

```bash
# Create a Pod | Generate Pod manifest Yaml. don't create it.
* kubectl run nginx --image=nginx
* kubectl run nginx --image=nginx --dry-run=client -o yaml

# Create a Deployment | Generate Deployment manifest Yaml. don't create it.
* kubectl create deployment --image=nginx nginx
* kubectl create deployment --image=nginx --dry-run=client -o yaml
```

## Imperative mode
```bash
kubectl run nginx-pod --image:nginx:alpine
kubectl run redis --image redis:alpine -l tier=db
kubectl expose pod redis --port=6379 --name redis-service

# Creating a deploymenty and scaling
kubectl create deployment webapp --image=nginx:alpine 
kubectl scale deployment/webapp --replicas=3

# Exposing a pod
kubect run custom-nginx --image=nginx port=8080

# Create a pod and a service to expose the pod
kubectl run http --image=httpd:alpine --port=80 --expose
```

### Kubetail
```bash
sudo apt-get install kubetail
```


### Exercises [Delete]
```bash
[1] Deploy a pod named nginx-pod using the nginx:alpine image.Use imperative commands only.

kubectl run nginx-pod --image=nginx:alpine --dry-run=client -o yaml > my-pod-01.yaml

[2] Deploy a redis pod using the redis:alpine image with the labels set to tier=db.


Either use imperative commands to create the pod with the labels. Or else use imperative commands to generate the pod definition file, then add the labels before creating the pod using the file.

kubectl run redis --image=redis:alpine --dry-run=client -o yaml

kubectl run redis --image=redis:alpine --dry-run=client -o yaml > my-pod-02.yaml

# then add labels tier=db

```

## About the CKAD  (Certified Kubernetes Application Developer)

- Core Concepts (13%)
- Multi-Container Pods (10%)
- Pod Design (20%)
- State Persistence (8%)
- Configuration (18%)
- Observability (18%)
- Services and Networking (13%)

## Note:
This repository have the notes of the courses that I took before my Kubernetes for Developer Certification
The courses that I took were:

* Udemy, Mumshad Mannambeth (highly recommended)
https://www.udemy.com/course/certified-kubernetes-application-developer/?start=0#overview

* Kuberenetes documentation
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/


* Pluranshit: Dan Wahlin
https://app.pluralsight.com/library/courses/kubernetes-developers-core-concepts/table-of-contents


* 42 Silicon Valley Bootcamp School
ft_services

* Curriculum for CKAD
https://github.com/cncf/curriculum/blob/master/CKAD_Curriculum_V1.20.pdf


# Articles
https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552