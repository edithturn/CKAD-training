
```bash

# Generate Deployment YAML file. Don't create it.
kubectl create deployment --image=nginx  nginx --dry-run -o yaml

# Save the Deployment YAML definition to a file.
kubectl create deployment nginx --image=nginx --dry-run=client \
-o yaml > nginx-deployment.yaml



# Generating Deployment with 03 Replicas
kubectl create deployment nginx --image=nginx --replicas=3

# Creating Deployment and scaling from 01 to 03
kubectl create deployment alpine --image=httpd:2.4-alpine

# Scale Deployment to 03 replicas
kubectl scale deployment alpine --replicas=3



# Deployment YAML definition



# Create a Deployment from YAML file.
kubectl create -f basic-deployment.yaml

# Update the Pod in the Deployment
kubectl set image deployment/nginx-deployment nginx=nginx:1.9.1



# Verify if the Deployment has failed to progress
kubectl rollout status deployment/nginx-deployment

# Check the revisions of a Deployment:
kubectl rollout history deployment/nginx-deployment

# Checking details of each revision
kubectl rollout history deployment/nginx-deployment --revision=1

# Undo the current rollout and rollback to the previous revision
kubectl rollout undo deployment/nginx-deployment

```