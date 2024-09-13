```bash
kubectl replace --force /tmp/kubectl-edit-2354563.yaml
kubectl get clusterroles --no-headers | wc -k
kubectl get nodes --as michelle

kubectl api-resources
```

k -n moon exec secret-handler -- env | grep SECRET1
k -n moon exec secret-handler -- cat /tmp/secret2/key
k -n moon exec secret-handler -- find /tmp/secret2
