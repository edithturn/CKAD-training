# **Pods**

**Pods** are a group of containers represented for deployable objects in Kubernetes. It could contain one or more containers.

## **Basic Commands**

```bash
# List pods in the default namespace
kubectl get pods

# List all the pods in al namespaces
kubectl get po --all-namespaces

# List pods in a particular namespace
kubectl get pods --namespace=dev
kubectl get po -n dev

# More details about all the Pods | Get the Ip address of the pod
kubectl get pods -o wide
kubectl get po nginx -o wide

# More details about a single Pod
kubectl describe pod basicpod

```

```bash
kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
myapp-pod   1/1     Running   1          33m
```

```bash
# Creating a pod
kubectl run nginx --image nginx

# Restart Never
kubectl run nginx --image nginx --restart=Never

# Specify the version of the image
kubectl run nginx --image=nginx:alpine
kubectl run redis --image redis123

# Creating pods based in yaml files
kubectl create -f my_pod.yml
kubectl apply -f /var/examples/my-pod.yaml
kubectl apply -f my-pod.yaml

# Creating pods in a specific namespace
kubectl create -f my-pod.yml --namespace=dev
kubectl run redis --image=redis --namespace=prod
kubectl run alpine --image=https:alpine -n limit
```

If we want to create a pod in diferent namespace, using yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
  namespace: dev
  labels:
    app: myapp
    type: front-end
spec:
  containers:
    - name: nginx-container
      image: nginx
```

```bash
# Edit a pod yml
vim 01-pod-definition.yml

# Get the yml file of the pod we just created
kubectl get pod nginx -o yaml

# Extract the definition to a file from a created Pod:
kubectl get pod nginx -o yaml > other-pod.yml

# Create a dry run of the Pod, It will not create the pod, but we can use the yaml to redirect the yamls definition into a file called pod.yaml
kubectl run redis --image=redis123  --dry-run=client -o yaml > pod.yaml

# Edit the file, and save the changes.
vim pod.yaml

# Apply to create the pod
kubectl apply -f pod.yaml

# Edit the file, and save the changes, add namespace=dev
vi pod.yaml
kubectl apply -f pod.yaml

# Other ways to edit a file, edit will automatically apply the changes
kubectl edit pod myapp-pod
kubectl edit pod redis
Nota: Only the properties listed below are editable
- spec.container[*].image
- spec.initContainer[*].image
- spec.activeDeadlineSeconds
- spec.tolerations
- spec.terminationGracePeriodSeconds

# Delete a pod, it will be created again by the deployment
kubectl delete pod pod-name

# Delete with the name of the file
kubectl delete -f nginx-pod.yml

# Delete Deployment that manages the Pod, this will delete the Pod definitelly
kubectl delete deployment pod-name

# Deliting all pods in a namespace
kubectl delete --all pods --namespace=dev

# Delete all the pods created
kubectl delete pod --all

# Delete the pod without any delay
kubectl delete pods nginx --grace-period=0 --force
```

## **More Commands**

```bash
# Create the nginx pod with version 1.17.4 and expose it on port 80
kubectl run nginx --image=nginx:1.17.4 --restart=Never --port=80

# Change the image version of the pod
kubectl set image pod/nginx nginx=nginx:1.15-alpine
kubectl set image pod/nginx nginx=nginx:1.17.1

#  Check the image version without the describe command
kubectl get po nginx -o jsonpath='{.spec.containers[].image}{"\n"}'

# Create the nginx pod and execute the simple shell on the pod
kubectl run nginx --image=nginx --restart=Never
kubectl exec -it nginx /bin/sh

# Create a busybox pod and run commands ls while creating it and check the logs
kubectl run busibox --image=busibox --restart=Never -- ls
kubectl logs busybox

# If pod ccrashed check the previous logs of the pod
kubectl logs busibox -p

# Create a pod with a command
kubectl run busibox --image=busibox restart=Never -- /bin/sh -c "sleep 3600"

# Create a busibox image pod and echo message "Hello! How are you?"
kubectl run busibox --image=nginx --restart=Never -it -- echo "Hello! How are you?"

# Create a pod busibox, show a message and then delete
kubectl run busybox --image=nginx --restart=Never -it --rm -- echo "Hello, How are you?"

# Create a nginx pod and list the pod with different levels of verbosity
kubectl run nginx --image=nginx --restart=Never --port=80

kubectl get po nginx --v=7
kubectl get po nginx --v=8
kubectl get po nginx --v=9

# List the pod with custom columns POD_NAME and POD_STATUS
kubectl get po -o=custom-columns="POD_NAME:.metadata.name, POD_STATUS:.status.containerStatuses[].state"

# List all the pods sorted by name
kubectl  get pods --sort-by=.metadata.name

# List all the pods created by timestamp
kubectl get pods--sort-by=.metadata.creationTimestamp
```

# FINAL

Pods are a group of containers represented for deployable objects in Kubernetes. A Pod could contain one or more containers (applications), one for the main process and one or more containers to “help” the main process.

# Get the documentation for Pod manifests

kubectl explain pods

# A basic Pod manifest basic-pod-manifest.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: static-web
  labels:
    role: myrole
spec:
  containers:
    - name: web
      image: nginx
      ports:
        - containerPort: 80
          protocol: TCP
```

# Creating pods based in YAML file

kubectl create -f basic-pod-manifest.yaml

# Get the YAML file of the Pod just created

kubectl get pod nginx -o yaml

# List Pods and their state in the default Namespace

kubectl get pods

# Get the definition of the Pod into a file

kubectl get pod static-web -o yaml > manifest.yml

# List all the Pods in all Namespaces

kubectl get pods --all-namespaces

# List Pods in a particular Namespace

kubectl get pods --namespace=dev

# Show more details about a single Pod

kubectl describe pod static-web

# Create a Pod using imperative commands

kubectl run nginx --image nginx

# Preview the object that would be sent to your cluster.

# Don't create the Pod

kubectl run nginx --image=nginx --dry-run=client -o yaml

# Edit a Pod

kubectl edit pod static-web

# Delete a pod

kubectl delete pod nginx

# Delete a pod force

kubectl delete pod nginx --force

# Pod logs

kubectl logs static-web -c web

# Pod port forwarding

kubectl port-forward static-web 8884:80

# execute the simple shell on the pod

kubectl exec -it static-web bash

# Connecting to the pod through the port forwarder:

curl localhost:8884
