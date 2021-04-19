```bash
# Deleting the previous element
kubectl delete --all pods --namespace=default
kubectl delete --all deployments --namespace=default
kubectl delete --all services --namespace=default
kubectl get all

# voting
kubectl create -f voting-app-deploy.yaml
kubectl create -f  voting-app-service.yaml
# Redis
kubectl create -f  redis-deploy.yaml
kubectl create -f  redis-service.yaml
# Postgres
kubectl create -f postgres-deploy.yaml
kubectl create -f postgres-service.yaml
# Worker
kubectl create -f worker-app-deploy.yaml

# Result
kubectl create -f  result-app-deploy.yaml
kubectl create -f  result-app-service.yaml

# Knowing the url
kubectl get all
minikube service voting-service --url
minikube service result-service --url
```