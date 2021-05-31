## Rolling Updates

When we create a deployment, it triggers a rollout, a new rollout created a new deployment revision.
Rolling update is the default deployment strategi


```bash
# Shot the revisions and history of our deployment
kubectl rollout status deployment/myapp-deployment
kubectl rollout history deployment/myapp-deployment
kubectl rollout undo deployment/myapp-deployment

```
```bash
#create
kubectl create -f deployment-definition.yml

# Get
kubectl get deployments

# Update
kubectl apply -f deployment-definition.yml
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1

# Status
kubectl rollout status deployment/myapp-deployment

# Rollback
 kubectl rollout history deployment/myapp-deployment

 kubectl rollout undo deployment/myapp-deployment
```

```bash
kubectl create -f deployment-definition.yml --record
```


## Rollbacks in Deployments
 