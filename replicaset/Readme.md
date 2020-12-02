# k8s-for-developers

## Example 01 | 01-replicaset-definition.yml
There are 03 sections more in the yml file:
* templates
* replicas
* selector

```bash
# Replica Set
kubectl create -f 01-replicaset-definition.ymlyml
kubectl get replicaset
kuebectl get pods
```

## Example 02 | 02-replicaset-definition.yml
Scaling the number of pods
* Updating the number of replicas from 03 to 06
```yml
replicas: 3
```
```yml
replicas: 6
```
After change the file, apply the change:
```bash
kubectl replace -f 02-replicaset-definition.yml
```
* Scaling
```bash
kubectl scale --replicas=6 -f replicaset-definition.yml

kubectl scale --replicas=6 replicaset myapp-replicaset
```