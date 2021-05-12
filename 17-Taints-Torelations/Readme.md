## Taints and Tolerations

```bash
kubectl taint nodes node-name key=value:taint-effect

```

Examples

```bash
k taint nodes node01 spray=mortein:NoSchedule

kubectl taint nodes node1 app=blue:NoSchedule
```
```yaml
apiVersion:
kind: Pod
metadata:
   name: myapp-pod
spec:
    containers:
    -  name: nginx-container
      image: nginx
    tolerations:
    - key: app
      operator: "Equal"
      value: "blue"
      effect: NoSchedule
```

## Tips

```bash
kubectl describe node node01 | grep -i taint

# Options for toleration
kubectl explain pod --recursive | less 

# 
kubectl describe nodes master | grep -i taint

kubectl taint node master node-role.kubernetes.io/master:NoSchedule-node/master untainted
```

# TODO