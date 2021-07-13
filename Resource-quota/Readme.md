# Resource Quota

## 01 example | 01-mem-cpu-demo.yml
```bash
# Create a quota from a ResourceQuota  definition
kubectl create -f mem-cpu-demo --namespace=dev

# Create a resource quota -> imperative
kubectl create quota myrq --hard=cpu=1,memory=1G,pods=2 --dry-run=client -o yaml

# View detailed information about the ResourceQuota:
kubectl get resourcequota mem-cpu-demo --namespace=dev --output=yaml
```

## 02 example | 02-quota-mem-cpu-pod.yml

```bash
# Create ResourceQuota for a Pod
kubectl create -f quota-mem-cpu-pod.yml --namespace=quota-mem-cpu-example

# Verity that the Pod's Container is running
kubectl get pod quota-mem-cpu-demo --namespace=quota-mem-cpu-example

# View detailed information about the ResourceQuota
kubectl get resourcequota mem-cpu-demo --namespace=quota-mem-cpu-example --output=yaml

```