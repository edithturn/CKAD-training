# ReplicaSet

## 01 example | 01-replicaset-definition.yml
There are 03 sections more in the yml file:
* templates
* replicas
* selector

```bash
# Replica Set
kubectl create -f 01-replicaset-definition.yml
kubectl get replicaset
kuebectl get pods
```

## 02 example | 02-replicaset-definition.yml
Scaling the number of pods, updating the number of replicas from 03 to 06 pods
```yml
# Before
replicas: 3
```
```yml
# After
replicas: 6
```
Then apply the change:
```bash
kubectl replace -f 02-replicaset-definition.yml
```
* Other ways to scaling
```bash
kubectl scale --replicas=6 -f replicaset-definition.yml

# TYPE: replicaset and NAME: myapp-replicaset
kubectl scale --replicas=6 replicaset myapp-replicaset
```