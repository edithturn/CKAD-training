## Ingress
k get deployments.apps --all-namespaces
k get ingress --all-namespaces
k describe ingress --namespace app-space

kubectl -n app-space describe i ingress-wear-watch
kubectl apply -f ingress.yaml
kubectl edit ingress --namespace app-space
k delete ingress ingress-wear-watch -n=app-space
k -n app-space delete ingress ingress-wear-watch
k apply -f /tmp/kubectl-edit-0n15v.yaml
k get services  --all-namespaces
k get deploy  --all-namespaces

kubectl get deployments.app, svc -n critical-space


# validate Service account


kubectl -n ingress-space get roles.rbac.authorization.k8.io
kubectl -n ingress-space get rolebindings.rbac.authorization.k8s.io

kubectl -n app-space describe ingress test-ingress

## Network Polices
kubectl get netpol
kubectl get pods -l name_payroll
kubectl get pods -l name=internal
kubectl describe netpol payroll-policy


