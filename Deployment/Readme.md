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
kubectl create deployment alpine --image=httpd:2.4-alpine
kubectl scale deployment alpine --replicas=3
kubectl scale deployment redis-deploy --replicas=2 -n dev-ns
```

## 01 example | deployment-definition.yml

```bash
# Create a deployment from YAML file.
kubectl create -f deployment-definition.yml
# List all deployments
kubect get deployments

# List deployments in a specific namespace
kubectl get deployments --namespace=develop


kubectl get replicaset
kubectl get pods
```

```bash
# Create a deployment with commands
kubectl create deployment http-frontend --image=httpd:2.4-alpine
```

## kubectl apply

```bash
# Apply and set image command in deployments
kubectl apply -f deployment-definition.yml

# Update the Pod in the Deployment
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
```

## Rollback

```bash
kubectl rollout status deployment/myapp-deployment

kubectl rollout history deployment/myapp-deployment

# The deployment will destroy the pods and create the other ones
kubectl rollout undo deployment/myapp-deployment

# Record in the revision history
kubectl edit deployment myapp-deployment --record
```

## More Commands

```bash
# Create a deployment with image nginx, 2 replicas and 80 port
kubectl create deploy nginx --image=nginx:1.18.0 --replicas=2 --port=80

# Describe the deploy or check replicaset
kubectl get rs -l run=nginx # if the deployment was created by 'run'
kubectl get rs -l app=nginx # if the deployment was created by 'create'

# Update the  nginx image to nginx:1.19.8
kubectl set image deploy nginx nginx=nginx:1.19.8

# Undo the latest rollout and verify that new pods have the old image
kubectl rollout undo deploy nginx

# Check a specific revision
kubectl rollout deploy nginx --revision=4

# Scale replicas
kubectl scale deploy --replicas=5

# Autoscale
kubectl autoscale deploy nginx --min=5 --max=10 --cpu-percent=80
# view the horizontalpodautoscalers.autoscaling for nginx
kubectl get hpa nginx
# Delete hpa
k delete hpa nginx
```
