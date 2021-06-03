## Labels
 Labels will help you put a TAG to a Kubernetes resource  to help you manage and identify the resource better

```bash
# Create a pod with label
kubectl run nginx1 --image=nginx --restart=never --labels=app=v1

# Show all the labels of the pods
kubectl get pods --show-labels

# Get pods of a specific label
kubectl get pods --selector app=App1

# Change the label of a specific pod
kubectl label nginx3 app=v2 --overwrite

# Get the label 'app' for the pods (show a column with APP label)
kubectl get pod -L app
kubectl get pod --lagel-columns=app

# Get pod for a specific label
kubectl get pod -l app=v2
kubectl get pod --selector=app=v2

# Delete a specific label
kubectl label pod nginx3 app-

# Add a label a node 
kubectl label nodes minikube accelerator=nvidia-tesla-p100

# Create a pod that will be deployed 
```

```bash
kubectl get pods -l env=dev
kubectl get pods -l env=dev --no-headers | we -l
```
```bash
 k get pods --selector bu=finance --no-headers | wc -l
get pods -l bu=finance --no-headers | wc -l
```
```bash
kubectl get -l env=prod --nno-headers
kubectl get all -l env=prod --nno-headers

kubectl get all -l env=prod --no-headers | wc -l 
```
```bash
kubectl get pods -l env=prod, bu=finance, tier=frontend
kubectl get all --selector env=prod,bu=finance,tier=frontend
```

## Selectors
Use Selectors to perform certain activities on resources with a particular label. 


## Annotations
Are ose to record other details for informatory purpose.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: annotations-demo
  annotations:
    imageregistry: "https://hub.docker.com/"
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80

```
```bash
k annotate po nginx1, nginx2, nginx3 description="My Pod Description"
# or
k annotate po nginx{1..3} description="My Pod Description"

# Check the annotation
k  describe po nginx1 | grep -i "description"

# Delete annotation
k annotate po nginx{1..3} description-
```