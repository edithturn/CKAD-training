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