# Taints and Torelations

- **Taints** are set on nodes
- **Toleration** are set in pods

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

## Creating a taint in a node

```bash
# Apply a taint to node01 that prevents new pods from being scheduled on it unless they tolerate the spray=mortein taint.
kubectl taint node node01 spray=mortein:NoSchedule
# Looking for taints
kubectl describe node node01 | grep -i taint
# Generates a YAML for a pod named "bee" that uses the "nginx" image, but it doesn't actually create the pod.
kubectl run bee --image=nginx --restart=Never --dry-run=client  -o yaml > bee.yaml

kubectl explain pod --recursive | less
kubectl explain pod --recursive | grep -A5 tolerations

```

```bash
# List all pods in a specifi Node
kubectl get pods --field-selector spec.nodeName=<node-name> -o wide
```

## Remove a Tain from a node

```bash
# List Tainst in another node
kubectl describe node controlplane | grep -i taint
# Taints:             node-role.kubernetes.io/control-plane:NoSchedule

# Remove the Taint from a node
kubectl taint nodes controlplane node-role.kubernetes.io/control-plane:NoSchedule-
```

## now which Node is a specific Pod

```bash
kubectl get pod <pod-name> -o jsonpath='{.spec.nodeName}'
```
