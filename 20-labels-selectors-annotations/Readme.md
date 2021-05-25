## Labels

```bash
# Get the pod with label information
kubectl get pods --show-labels

# Get pods of a specific label
kubectl get pods --selector app=App1
```

```bash
kubectl get pods -l env=dev
kubectl get pods -l env=dev --no-headers | we -l
```

```bash
 k get pods --selector bu=finance --no-headers | wc -l
get pods -l bu=finance --no-headers | wc -l
```

```bash
kubectl get -l env=prod --nno-headers
kubectl get all -l env=prod --nno-headers

kubectl get all -l env=prod --no-headers | wc -l 

```

```bash
kubectl get pods -l env=prod, bu=finance, tier=frontend
kubectl get all --selector env=prod,bu=finance,tier=frontend

```
