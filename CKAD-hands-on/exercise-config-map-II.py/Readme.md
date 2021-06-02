## **Problem**
1. Create a new namespace to work from 
2. Create a file and store the text "Hello, world!" in the file
3. Create a ConfigMap with a variable called "greeting" with a value pointing to the file previously created
4. Create a new BusyBox box deployment with 5 replicas and expose the config map variable greeting as a an environmet variable called "MY_GREETING". Pass the command 'env' to the running containers and stop each of the containers from exiting.

5. Once deployed and running, get lofs one of the pods and verify the key/value pairs in the file from step 1 are being use

6. Clean aup all resources created

## **Solution**
```bash
# Create a new namespace
kubectl create namespace my-namespace

# Set the context to the current namespace
kubectl config set-context --current --namespace=my-namespace

# Create Config Map and it should take a variable from a file
kubectl create cm task-cm --from-file=greeting=file

# See the Config Maps
kubectl get cm

# Create a deployment with 5 replicas using busybox image
kubectl create deployment task-deploy --image=busybox --replicas=5 --dry-run=client -o yaml > deploy.yaml

# Edit the deploy and add the config map, command and args
vim deploy.yaml

# Create the deploy
kubectl apply -f deploy.yaml

# Cehck the logs 
kubectl logs pod/my-dep-6f6d4dddb5-8kcdf

# Clean the namespace
kubectl delete ns edithns
```

