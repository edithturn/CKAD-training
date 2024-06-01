```bash
# Check the Labels exist in a node
k describe node
```

```bash
# Check the pods in a specific node
kubectl get pods --field-selector spec.nodeName=<node-name> -o wide
```
