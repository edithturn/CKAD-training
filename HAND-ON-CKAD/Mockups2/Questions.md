## **Problem 01**
Create a deployment called my-webapp with image: nginx, label tier:frontend and 2 replicas. Expose the deployment as a NodePort service with name front-end-service , port: 80 and NodePort: 30083

## **Solution**
```bash
# Create de Deployment
kubectl create deploy my-webappp --image=nginx  --replicas=2

# Then edit the deployment to add a label
kubectl edit deployments.apps my-webapp

# Add the label and save the changes, see the complete deplyoment 01-my-webapp.yaml
```
```yaml
labels:
    tier: frontend
```

```bash
# Then expose the deployment as a NodePort service with name front-end-service, port 80 and NodPort 30083
kubectl expose deployment my-webapp --name=front-end-service --type=NodePort --target-port=80 --port=80 --dry-run=client -o yaml > sv.yaml

# Then edit the Service yaml
vim sv.yaml
Add the nodeport: 30083

# Now create the service
kubectl apply -f sv.yaml
```
## **Problem 02**
Add a taint to the node node01 of the cluster, 
key:app_type, value: alpha and effect: NoSchedule
Create a pod called alpha, image: redis with toleration to node01

## **Solution**

```bash
# Check the nodes
kubectl get nodes

# Create the taint
kubectl taint nodes node1 'app_type=value1:NoSchedule'

# Create the pod
kubect run alpha --image=redis --dry-run -o yaml > alpha.yaml

# Edit the yaml to add the toleration and create the pod
vim alpha.yaml
```
```yaml
  tolerations:
  - key: "app_type"
    operator: "Equal"
    effect: "NoSchedule"
    value: alpha
```
```bash
# The create the pod
kubectl apply -f alpha.yaml

# Check the result, check the NODE column
kubectl get pod alpha -o wide
```

* Note: To remove the taint in a node use:
```bash
kubectl taint nodes node1 key1=value1:NoSchedule-
```


## **Problem 03**
Apply a label app_type=beta to node node02. Create a new deployment called beta-apps with image:nginx and replicas:3. Set Node Affinity to the deployment to place the PODs on node02 only



## **Solution**
```bash
# Create a label on node02
kubectl label node node02 app_type=beta

# Create a new deployment
kubectl create deployment beta-apps --image=nginx --replicas=3 --dry-run=client -o yaml > deploy.yaml

# Update the yaml and add nodeAffinity
vim deploy.yaml
```
```yaml
    affinity:
      nodeAffinity:
         requiredDuringSchedulingIgnoredDuringExecution:
           nodeSelectorTerms:
           - matchExpressions:
             - key: app_type
               operator: In
               values:
               - beta
```


## **Problem 04**
Create a new Ingress Resource for the service: my-video-service to be made available at the URL: http://ckad-mock-exam-solution.com:30093/video.


## **Solution**

```bash
kubectl get svc

kubectl describe svc my-video-service

# Create a ingress
vim ingress.yaml
 
```
## **Problem 05**
## **Problem 06**
## **Problem 07**

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: custon-volume
spec:
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: /opt/data
```
k create -f pv.yaml
k get pv
