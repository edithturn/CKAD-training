## Service Account
```bash
kubectl create serviceaccount dashboard-sa

kubectl get serviceaccount

kubectl describe serviceaccount dashboard-sa

kubect describe secret dashboard-sa-token-kbbdm
```

```bash
kubectl exec -it my-kuberntes-dashboard ls /var/run/secrets/kubernetes.io/serviceaccount

kubecctl exec -it my-kubernetes-dashboard cat /var/run/secrets/kuberentes.io/servicesaccount/token
```


```yaml
apiVersion: v1
kind: Pod
metadata:
   name: my-kubernetes-dashboard
spec:
   containers:
      - name: my-kubernetes-dashboard
        image: my-kubernetes-dashboard
    serviceAccount: dashboard-sa
```