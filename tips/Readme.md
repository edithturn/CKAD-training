# Tips and Tricks to help you to pass certified Kubernetes Application Developer (CKAD)


Use alias
```bash
alias k=kubectl
alias krd kubectl run --dry-run=client -o yaml # then use it: krd --image=nginx > pod.yaml
```

We can find more abbreviates using: **kubectl api-resources**
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
```kubectl
# Everytime to delete the pod 
alias kdp='kubectl delete pod pod --farce --grace-period=0'
```


```bash
kubectl get all
```
### Shot the revisions and history of our deployment
```bash
kubectl rollout status deployment/,yapp-deployment
kubectl rollout history deployment/myapp-deployment
```

**If you are in minikube**
You want to know the url of a services type: 
```bash
minikube service voting-service --url h
# Result
http://192.168.49.2:30004
```

### Alias
```bash
alias kdp='kubectl delete pod --force --grace-period=0'
```

### Use the correct context to set us in a cluster

```bash
# Every time before to start the question
kubectl config use-contex CONTEXTNAME
```

### Generate a preview without a file
```bash
kubectl create namespace test-123 --dry-run=client -o json
kubectl create namespace test-123 --dry-run=client -o yaml

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
   
### Source:
* https://kubernetes.io/docs/reference/kubectl/cheatsheet/



### Logs

```bash

kubectl logs webapp-1 | grep USER5
# to select the containers
kubectl logs webapp-2 -c
kubectl logs webapp-2 -c simple-webapp

```

### Monitoring
```bash
kubectl top node
kubectl top pod
```

watch "kubectl top node"
