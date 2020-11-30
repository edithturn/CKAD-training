# Kubectl


### Basic commands
```bash
* kubectl api-resources
* kubectl create -f basic.yaml
* kubectl get pod
* kubectl  describe pod basicpod
* kubectl get pod -o wide
```

### Expose the port to the clister
```bash
# Adding type NodePort in the service
* kubectl delete basicpod ; kubectl create -f basic.yaml
* kubectl create deployment firstpod --imagee=nginx
* kubectl get deployment, pod
* kubectl get namespaces
* kubectl get pod -n kube-system
* kubectl get pod -n default

# View resources in all namespaces at once. 
* kubbectl get pod --all-namespaces
* kubectl get deploy, rs, po, svc,ep

# Delete the top-level controller
kubectl delete deployment firstpod
```

### Build using a local Docker Registry

```bash
* kubectl create deployment <Deploy-Name> --image=<repo>/<app-name>:<version>
* kubectl create deployment time-date --image=10.110.186.162:5000/simpleapp:v2.2

# Iteractive shell:
* kubectl exec -i​t <Pod-Name> -- /bin/bash

# Logs
* kubectl logs test1
* kubectl -n kube-system logs etcd-ckad-1

# Become root using sudo
sudo -i
```

### Creating volumes
```bash
* kubectl create -f vol2.yaml
* kubectl get pv
```

### Converting a docke-compose file into yaml
sudo kompose convert -f docker-compose.yaml -o localregistry.yaml


### Create deployment
```bash
kubectl create deployment drytry --image=nginx --dry-run=client -o yaml

sudo docker tag ubuntu:latest 10.110.186.162:5000/tagtest
sudo docker pull 10.110.186.162:5000/tagtest

kubectl create deployment try1 --image=10.110.186.162:5000/simpleapp
kubectl scale deployment try1 --replicas=6

```

### Kubernetes Liveness and Readiness Probes


