# Services
```bash
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml

kubectl create service nodeport nginx --tcp=80:80 --node-port=30087 --dry-run=client -o yaml
```