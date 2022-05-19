# Services
A Kubernetes Service is a way to create a single, constant point of entry for a group of Pods through a network service.


# Kind of Services
1.  NodePort: Exposes a service via a static port on each node's IP.
  **TargetPort**, is the port on which your container is running.
  **Port**, port redirects the traffic to the container from the service.   
  **NodePort**,: is the port that enables the service to access the externally.

2. ClusterIp : Exposes a service which is only accessible from within the cluster.

3. LoadBalancer: Exposes the service via the cloud provider's load balancer.
4. ExternalName:  Is a special case of Service that does not have selectors and uses DNS names instead

Example: service-example.yaml

```yaml

apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376

```

# Basic Commands

```bash


kubectl get services
kubectl get svc
kubectl describe service my-service



kubectl expose pod redis --port=6379 --name redis-service
kubectl expose pod httpd --port=80
kubectl create service clusterip redis --tcp=6379:6379 
kubectl create service nodeport nginx --tcp=80:80 --node-port=30087

```


```bash



# Create a new NodePort service named my-ns
kubectl create service nodeport my-ns --tcp=5678:8080
#Create a new ClusterIP service named my-cs
kubectl create service clusterip my-cs --tcp=5678:8080
# Create a new LoadBalancer service named my-lbs
kubectl create service loadbalancer my-lbs --tcp=5678:8080
# Create a new ExternalName service named my-ns
kubectl create service externalname my-ns --external-name bar.com




```



