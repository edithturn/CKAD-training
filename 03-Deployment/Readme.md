# Deployments

```bash
# Generate Deployment Yaml file (-o yaml). Don't create it (--dry-run)
kubectl create deployment --image=nginx  nginx --dry-run -o yaml

# Generating deployment with 03 Replicas
kubectl create deployment nginx --image=nginx --replicas=3
kubectl create deployment httpd-frontend --image=httpd:2.4-alpine --replicas=3
# Scaling a deployment 
kubectl scale deployment nginx --replicas=4
```

## 01 example | deployment-definition.yml
```console
kubectl create -f deployment-definition.yml
kubect get deployments
kubectl get replicaset
kubectl get pods
```

```console
# Create a deployment with commands
kubectl create deployment http-frontend --image=httpd:2.4-alpine
```
## Lubectl Apply
```console
# Apply and set image command in deployments
kubectl apply -f deployment-definition.yml
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
```

## Rollback 
```console
kubectl rollout status deployment/myapp-deployment
kubectl rollout history deployment/myapp-deployment
# The deployment will destroy the pods and create the other ones
kubectl rollout undo deployment/myapp-deployment
```
