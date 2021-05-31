## Solution

```bash
kubectl run my-busybox --image=busybox --command sleep 3600 --dry-run -o yaml > busybox.yaml

# Edit the pod yaml and add volumeMounts and secret as a volume
vim busybox.yaml

```

```bash

```


```bash

```
