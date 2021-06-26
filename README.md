# CNCF’s CKAD certification - Cloud Native Computing Foundation

<p align="center">
  <img width="500" height="350" src="img/k8s.png">
</p>


# `` REPOSITORY IN PROGRESS ... `` :carousel_horse: :raising_hand:  :tractor:

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


### Kubetail
```bash
sudo apt-get install kubetail
```


## **Suggestions - CKDA Udemy course with Mumshad**
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

## **Tips on preparing for CKAD - Muralidaran shanmugham**
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
  - know all the commands =>  [HERE](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-getting-started-strong-) 
  - --restart (YAML generator)
  - args: ["-c", "while true; do date >> /var/log/app.txt; sleep 5; done"]
  - args: [/bin/sh, -c, 'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done']
  - args: ["-c", "mkdir -p collect; while true; do cat /var/data/*> /collect/data.txt; sleep 10; done"]
  - Use of grep:
    - kubectl describe pods | grep --context=10 annotations:
    - kubectl describe pods | grep --context=10 Events:                                                                          
## Tips for VIM
```bash
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
```


### Be fast Ingress
```bash
kubectl get all --all-namespaces

kubectl get deploy --namespace app-space
kubectl get deployments.app -n=app-space

kubectl get ingress --all-namespaces
kubectl describe ingress --namespaces app-space
kubectl edit ingress --namespace app-space
```

## Use Alias
```bash
alias k='kubectl'
alias krd='kubectl run --dry-run=client -o yaml' # then use it: krd --image=nginx > pod.yaml
alias kcd='kubectl create --dry-run=client -o yaml' # then use it: krd --image=nginx > pod.yaml
alias kdp='kubectl delete pod --force --grace-period=0'
alias kaf='kubectl apply -f'
alias kaf='kubectl create -f'
alias kns='config set-context --current --namespace'
```

## Use Completions
Documentation [here](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-autocomplete)
```bash
alias k=kubectl
complete -F __start_kubectl k
```

## Create bookmarks on Chrome
- Go to the documentation
- Select a topic
- Go to specific section of the page 
- Set a bookmark
- If you need copy the code, use copy application to clipboard

### Use the correct context to set us in a cluster

```bash
# Every time before to start the question
kubectl config use-contex CONTEXTNAME
```

## Abbreviates using: 
Find more with "kubectl api-resources"
```bash
k get ns        # for namespaces
k get deploy    # for deployments
k get pv        # for persistentvolumes
k get pvc       # for persistentvolumeclaims
k get svc       # for services
k get no        # for nodes
k get po        # for pods
k get cj        # for cronjobs
k get quota     # for resourcequotas
```

```bash
kubectl get all
```

### Generate a preview without a file
```bash
kubectl create namespace test-123 --dry-run=client -o yaml
```

### Updating existing resources

* **edit** will apply any change in the current resource after update the yaml
```bash
kubectl edit pod nginx
kubectl edit deployment app
```
* **set** will update a version in a pod or deployment
```bash
kubectl set image pod/nginx nginx=nginx:latest
kubectl set image pod/nginx nginx=nginx:1.9.1
kubectl set image deployment/nginx nginx=nginx:latest
kubectl set image deployment/nginx nginx=nginx:1.9.1
```

## Log and Debuggind
```bash
k run --image=busybox bbox -- sh -c 'while true; do date; sleep 3; done '
# To keep watching the logs
kubectl  logs bbox --follow

# Use describe
kubectl describe bbox
kubectl describe mydeploy

# Se the event for all the resources
kubectl get events

#Use grep
k get events | grep Schedule

# View control exec
kubectl run --image=busybox bbox -- sh -c 'echo here; sleep 3600'
# Access to the shell inside the pod
kubectl exec -it bbox -- sh
ls
exit
```

## Be faster

```bash
# Check all the deployments in all the namespaces
k get get deploy --all-namespaces

# 
k run yellow --image=busibox --restart=never --dry-run -o yaml  > pod.yml
vi pod.yaml
kubectl apply -f pod.yml
kubectl describe pod yellow

# check namespace just creates, take the one that was reciently created
kubectl get ns
kubectl -n elastic-stack get pod, svc
```

```bash
kubectl -n elastic-stack get pod-svc

```

```bash
kubectl -n elastic-stack get pod app -o yaml > app.yaml
kbuectl delete pod app -n elastic-stack
vi app.yaml
```
## Extra commands
```bash
ps -aux
ps -aux | grep -i 'string'
ps -aux | grep -e 'exp-one' -e 'exp-two'
ifconfig
ip a
ip r
systemctl status kubelet
systemctl restart kubelet
systemctl daemon reload
journalctl -u kubelet
netstat -tunlp

```
### Logs

```bash
kubectl logs webapp-1 | grep USER5
# to select the containers
kubectl logs webapp-2 -c
kubectl logs webapp-2 -c simple-webapp
kubectl logs alta3pod | sudo tee ~/opt/answers/mypod.log
```

### Monitoring
```bash
kubectl top node
kubectl top pod
```


## Resources:
* [Udemy CKAD preparation](https://www.udemy.com/course/certified-kubernetes-application-developer/?start=0#overview) -> Mumshad Mannambeth
* [Kuberenetes documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) All my bookmarks.

## Practice:

1. [How to Prepare for CKAD and CKA Certification?](https://www.infracloud.io/blogs/prepare-cka-ckad-certification/) -> InfraCloud Team
2. [Game of Pods](https://kodekloud.com/p/game-of-pods-game) A set of fun challenges to learn and practice your skills on Kubernetes
3. [Kubernetes CKAD Example Exam Questions Practical Challenge Series](https://codeburst.io/kubernetes-ckad-weekly-challenges-overview-and-tips-7282b36a2681) -> Kim Wuestkamp
4. [Practice Enough With These 150 Questions for the CKAD Exam](https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552)  -> Bhargav Bachina
5. [CKAD Exercises](https://github.com/dgkanatsios/CKAD-exercises) Github -> dgkanatsios
6. [Kubernetes Network Policy Recipes](https://github.com/ahmetb/kubernetes-network-policy-recipes)
7. [katacoda - CKAD Practice Challenge](https://www.katacoda.com/liptanbiswas/courses/ckad-practice-challenges)
8. More Practice (Trial)
https://www.study4exam.com/

## Videos 

1. [How to Pass CKA, CKAD with Flying Colors?](https://www.youtube.com/watch?v=TJSAcwUP0pE)    -> I AM DINUTH
2. [How to CRUSH the CKAD Exam!](https://www.youtube.com/watch?v=5cgpFWVD8ds) -> Alta3 Research, Inc.
3. [Vim Crash Course | How to edit files quickly in CKAD / CKA exam](https://www.youtube.com/watch?v=knyJt8d6C_8) -> The FrontOps Guy


