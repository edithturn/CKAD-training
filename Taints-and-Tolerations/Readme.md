# Taints and Torelations

* **Taints** are set on nodes
* **Toleration** are set in pods



```bash
kubectl taint nodes node-name keyt=value:taint-effect
kubectl taint nodes node1 app=my_app: NoSchedule
```

### Telerations - Pods

```yaml
apiVersion:
kind: Pos
metadata:
  name: myapp-pod
spec:
  containers:
  - name: nginx-container
    
  tolerations:
  - key: "app"
    aperator: "Equal"
    value: "blue"
    effect: "NoSchedule"
```


Looking for taints
```bash
kubectl describe node node01 | grep -i taint
```

## Creating a taint in a node

```bash
kubectl taint node node01 spray=mortein:NoSchedule
kubectl describe node node01 | grep -i taint
kubectl run bee --image=nginx --restart=Never --dry-run  -o yaml > bee.yaml

kubectl explain pod --recursive | less

kubectl explain pod --recursive | grep -A5 tolerations

```