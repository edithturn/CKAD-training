```bash
kubectl replace --force /tmp/kubectl-edit-2354563.yaml
kubectl get clusterroles --no-headers | wc -k
kubectl get nodes --as michelle

kubectl api-resources
```

k -n moon exec secret-handler -- env | grep SECRET1
k -n moon exec secret-handler -- cat /tmp/secret2/key
k -n moon exec secret-handler -- find /tmp/secret2

````



```bash
kubectl logs -n ckad-multi-containers pods/static-web-server main-container
````

more complext commands:

```bash
k run ckad-ubuntu-qwfefefwe -n ckad-pod-design --image=ubuntu $do --command -- /bin/sh -c "sleep 3600"  > 4-pod.yaml
```

```bash
kubectl get pods -A -o=custom-columns='POD_NAME:metadata.name,IP_ADDR:status.podIP' --sort-by=.status.podIP > /root/pod_ips_ckad02_svcn
```
