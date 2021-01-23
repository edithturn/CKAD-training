# Deployments

```bash
# Generate Deployment Yaml file (-o yaml). Don't create it (--dry-run)
kubectl create deployment --image=nginx  nginx --dry-run -o yaml

# Generating deployment with 03 Replicas
kubectl create deployment nginx --image=nginx --replicas=3

# Scaling a deployment 
kubectl scale deployment nginx --replicas=4
```

## 01 example | deployment-definition.yml
```bash
kubectlcreate -f deployment-definition.yml
kubect get deployments
kubectl get replicaset
kubectl get pods
```

```bash
# Create a deployment with commands
kubectl create deployment http-frontend --image=httpd:2.4-alpine
```