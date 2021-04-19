 ```bash
 # Creating pods and services
 kubectl create -f voting-app-pod.yaml
 kubectl create -f voting-app-service.yaml
 minikube service voting-service --url
 kubectl create -f redis-pod.yaml
 kubectl create -f redis-service.yaml

 #Listing kubernetes elements
 kubectl get pods,svc
 kubectl create -f postgres-pod.yaml
 kubectl create -f postgres-service.yaml
 kubectl create -f worker-app-pod.yaml
 kubectl create -f result-app-pod.yaml
 kubectl create -f result-app-service.yaml 
 # Showing the service url
 minikube service voting-service --url
 minikube service result-service --url
```