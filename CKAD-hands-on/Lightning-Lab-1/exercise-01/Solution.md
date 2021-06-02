## **Problem**

Create a Persistent Volume called log-volume. It should make use of a storage class name manual. It should use RWX as the access mode and have a size of 1Gi. The volume should use the hostPath /opt/volume/nginx

Next, create a PVC called log-claim requesting a minimum of 200Mi of storage. This PVC should bind to log-volume.

Mount this in a pod called logger at the location /var/www/nginx. This pod should use the image nginx:alpine.

## **Solution**

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