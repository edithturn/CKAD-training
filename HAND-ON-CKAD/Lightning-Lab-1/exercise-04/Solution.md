## **Problem**
Create a new deployment called nginx-deploy, with one signle container called nginx, image nginx:1.16 and 4 replicas. The deployment should use RollingUpdate strategy with maxSurge=1, and maxUnavailable=2.
Next upgrade the deployment to version 1.17 using rolling update.
Finally, once all pods are updated, undo the update and go back to the previous version.


## Solution

**Create the deploy with 01 replicas**
export do="--dry-run=client -o yaml"
```bash
kubectl create deploy nginx-deploy --image=nginx:1.16 $do > deploy.yaml

# Add replicas = 4 , add strategy of rollback
vim depoy.yaml

# Create the deploy
kubect apply -f deploy.yaml
```

**Update the version of the image to nginx=nginx:1.7**
```bash
# Changing the image to 1.7
kubectl set image deployment/nginx-deploy nginx=nginx:1.7

# Checking the image version
kubectl describe deploy nginx-deploy | grep -i ima
Image:        nginx:1.16

# Then rollout the to the previous version
kubectl rollout history deploy nginx
```