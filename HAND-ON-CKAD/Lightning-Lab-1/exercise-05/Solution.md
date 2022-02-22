## **Problem**

Create a redis deployment with the following parameters:
Name of the deployment should be redis using the redis:alpine image. It should have exactly 1 replica.
The container should request for .2 CPU. It should use the label app=redis.
It should mount exactly 2 volumes:
Make sure that the pod is scheduled on master/controlplane node.


a. An Empty directory volume called data at path /redis-master-data.
b. A configmap volume called redis-config at path /redis-master.
c.The container should expose the port 6379.


The configmap has already been created.

## **Solution**

```bash
# Create the deployment
kubectl create deploy redis --image=redis:alpine --dru-run=client -o yaml > deploy.yaml

# Edit the file, to add .2 CPU and labels app=redis and, add the two volumes
kubectl vim deploy.yaml

# Crate the depoyment
kubectl apply -f deploy.yaml
```