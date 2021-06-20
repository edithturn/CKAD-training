# **Tips and Tricks for CKAD**

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
linq closes

## Use Completions <- My Favorite
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
