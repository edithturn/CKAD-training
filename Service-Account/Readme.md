# Service Account

A service account in Kubernetes is a special type of account not linked to a person. It gives a unique identity to application pods, system components, and other entities within or outside the cluster. These entities use the service account's credentials to authenticate and access the Kubernetes API server or apply security policies based on identity. This ensures secure and controlled access to resources.

## Imperative Commands

```bash
kubectl create serviceaccount dashboard-sa

kubectl create sa ingress-serviceaccount -n ingress-space
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

To create token

```bash
kubectl create token dashboard-sa
```
