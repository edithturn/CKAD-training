# Deployments

```bash
# Generate Deployment Yaml file (-o yaml). Don't create it.
kubectl create deployment --image=nginx  nginx --dry-run -o yaml

# dry-run
kubectl create deployment webapp --image=kodekloud/webapp-color --replicas=3  --dry-run=client -o yaml

kubectl create deployment webapp --image=kodekloud/webapp-color --replicas=3  --dry-run=client -o yaml > my-pod-04.yaml

kubectl apply -f my-pod-04.yaml

# Another way to save the YAML definition to a file.
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml

# Generating deployment with 03 Replicas
kubectl create deployment nginx --image=nginx --replicas=3
kubectl create deployment httpd-frontend --image=httpd:2.4-alpine --replicas=1

# Creating deployment and scaling from 01 to 03
kubectl create deployment httpd-frontend --image=httpd:2.4-alpine
kubectl scale deployment nginx --replicas=3
kubectl scale deployment redis-deploy --replicas=2 -n dev-ns
```

## 01 example | deployment-definition.yml
```console
kubectl create -f deployment-definition.yml
kubect get deployments
# Looking deployments in a specific namespace
kubectl get deployments --namespace=default
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

# Record in the revision history
kubectl edit deployment myapp-deployment --record
```
