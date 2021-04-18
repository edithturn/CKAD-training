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
