# Service
The Service is like a server inside the node. It can expose a port for users or for other applications.


# Kind of Services
* NodePort
* ClusterIp
* LoadBalancer
* ExternalName



# 1.  Service - NodePort
  **TargetPort**, the node of the pod
  **Port**, the port of the node   
  **NodePort** => It could be any value between 3000 and 32767, this is the port on the node on which the application will be accesible

**Definition**
```yml
apiVersion: v1
kind: Service
metadata:
   name: myapp-service
spec:
   type:  NodePort
   ports:
   - targetPort: 80
     port: 80
     nodePort:  30008
   selector:
     app: myapp
     type: front-end
```

Notes: 
* To link the node port with the pod port we need labels and selectors. We can use the labels of the pod and put it in the selector section on the Service yml

**What happen if the node has several pods?**
Kubernetes use the random algorithm to balance the load across the three  different pods.

### Basic Commands
```bash
# Create the Service
kubectl create -f 00-service-definition.yml

# Create a service with expose
kubectl expose deployment simple-webapp-deployment --name=webapp-service --target-port=8080 --type=NodePort --port=8080 --dry-run=client -o yaml > svc.yaml

# Apply changes
kubectl apply -f 00-service-definition.yml

# List Services
kubectl get services
kubectl get svc

# List all the services in the particular namespace
kubectl get svc -n dev

# Listing Services in a specific namespaces
kubectl -n dev get svc
kubectl -n dev get services

# Another way to list more than one element
kubectl get pods, svc
kubectl describe service kubernetes
```
Note:
After create the Service we can access to the pod with the IP od the Node and the nodPort number:
```bash
curl http://192.1683.1.2:30008
```

# 2. Service - ClusterIp
**Definition**
```yml
apiVersion: v1
kind: Service
metadata:
    name: backend
spec:
    type: ClusterIp
    ports:
      - targetPort: 80
        Port: 80
    selector:
      app: myapp
      type: back-end
```
Note: ClusterIp is the default type, if we don't specify this will take the kind of ClusterIp automatically


# 3. Service - LoadBalancer
Set the Service type in LoadBalancer, it works on GCP, Azure, AWS

**Definition**
```yml
apiVersion: v1
kind: Service
metadata:
    name: backend
spec:
    type: LoadBalancer
    ports:
      - targetPort: 80
        Port: 80
    selector:
      app: myapp
      type: back-end
```


# Examples
```bash
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

kubectl expose pod httpd --port=80 --name httpd --dry-run=client -o yaml > yy.yaml

kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml

kubectl create service nodeport nginx --tcp=80:80 --node-port=30087 --dry-run=client -o yaml
```

