# Deployments

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