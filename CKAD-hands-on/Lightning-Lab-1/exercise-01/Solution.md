## Solution

### Persistet Volume
```bash
kubectl create -f pv.yaml
```

### Persistet Volume Claim

```bahs
kubectl create -f pvc.yaml
```

### Pod with Volume

```bash
kubectl run --generator=run-pod/v1 logger --image=nginx:alpine --dry-run=client -o yaml > pod.yaml

Kubectl run run-pod --image=nginx  -o yaml --dry-run=client > pod.yaml

# Edit pod and add volumeMounts and volumes
kubctl vim pod.yaml
kubectl apply -f pod.yaml
```