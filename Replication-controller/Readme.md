# Replication Controller

## Replication Controller | Replica Set 

The major difference between replication controller and replica set. 
is **selector**
"Selector" is requeired in replica set.
*ReplicaSet is the new recommended way for scaling*

* Replication controller is possible just with a node, is possible to depele the previous pod and create a new one

```bash
# Replication Controller
kubectl create -f rc-definition.yaml
kubectl get replicationcontroller
kuebectl get pods
```

```bash
# Replica Set
kubectl create -f rc-definition.yaml
kubectl get replicationcontroller
kuebectl get pods

# Also delete all the pods into this replicaset
kubectl delete replicaset myapp-replicaset
kubectl replace -f replicaset-definitionyml
kubectl scale -replicas=6 -f replicaset-definition.yml
```

## 01 example 01 | rc-definition.yml

```bash
# Replication Controller
kubectl create -f rc-definition.yml
kubectl get replicationcontroller
kuebectl get pods
```