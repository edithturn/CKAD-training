# Kubernetes For Developers - CKAD

<p align="center">
  <img width="500" height="350" src="img/k8s.png">
</p>


# `` REPOSITORY IN PROGRESS ... `` :carousel_horse: :raising_hand:  :tractor:

## Componentes Of Kubernetes
- API Server
- etcd
- kubelet
- Container Runtine
- Controller
- Scheduler

## Architecture
  A node is a machine physical or virtual, and node is a worker machine and that is where containers will be launched by Kubernetes.

## About the CKAD  (Certified Kubernetes Application Developer)

- Core Concepts (13%)
- Multi-Container Pods (10%)
- Pod Design (20%)
- State Persistence (8%)
- Configuration (18%)
- Observability (18%)
- Services and Networking (13%)


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
* kubectl get pod --all-namespaces
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


## Suggestions [source - CKDA udemy course from Mumshad]
* Attempt all questions
* Don't get stuck on any question
* Get good with YAML
* Use shortcuts/aliases
  - po for PODS
  - rs for RepicaSets
  - deploy for Deployments
  - svc for Services
  - ns for Namespaces
  - netpol for Networking polices
  - pv for Persistent Volumes
  - pvc for PersistentVolumeClaims 
  - sa for service accounts

## Other suggestions [source Muralidaran shanmugham - Tips on preparing for Certified Kubernetes Application Developer (CKAD)
]
* Go through the k8s.io documentation
* Understand all the concepts outlined in the exam curriculum
* Register for courses like Kodekloud
* Time management
  - nano Editor
  - Kubectl alias
  - learn shortcuts
  - alias k='kubectl'
  - k config set-context <cluster name> --namespace=<namespace name>
  - k explain cronjob.spec.jobTemplate --recursive
  - know all the commands =>   https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-getting-started-strong-
  - --restart (YAML generator)
  - args: ["-c", "while true; do date >> /var/log/app.txt; sleep 5; done"]
  - args: [/bin/sh, -c, 'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done']
  - args: ["-c", "mkdir -p collect; while true; do cat /var/data/*> /collect/data.txt; sleep 10; done"]
  - Use of grep:
    - kubectl describe pods | grep --context=10 annotations:
    - kubectl describe pods | grep --context=10 Events:                                                                          
    
## Tips for VIM
* Use h -> move to left, l - > move to right, j -> move down , k -> move  up
* Esc + DD        | delete a line
* Esc + o         | add a new line
* Esc + w         | move word to word, set cursosr at the beginning of the word
* Esc + e         | move word to word, set cursor at the end of the word
* Esc + :set num  | to add line numbers
* Esc + y         | copy a line
* Esc + p         | paste the line
* Shift + v       | to visual mode and  up and down arrows to move the cursor
* Shift + >       | Indentation to the right
* Shift + <       | Indentation to the left
* Esc + u         |  revert changes
* ALT + f         | move the cursor after the word
* ALT + b         | move the cursos before the word
* Esc + dw        | Delete a word
* Esc + /         | Find a word
* o               | Yo add a new empty line in a yaml


## TIPS

Be fast Ingress
```bash
kubectl get all --all-namespaces

kubectl get deploy --namespace app-space
kubectl get deployments.app -n=app-space

kubectl get ingress --all-namespaces
kubectl describe ingress --namespaces app-space
kubectl edit ingress --namespace app-space
```
Logs
```bash
kubectl logs alta3pod | sudo tee ~/opt/answers/mypod.log


```

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


# Game of Pods
https://kodekloud.com/p/game-of-pods-game

# Articles
https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552

# Exercises
https://github.com/dgkanatsios/CKAD-exercises

## Videos
How to CRUSH the CKAD Exam!
https://www.youtube.com/watch?v=5cgpFWVD8ds