## Ingress Controller
    - Deployment
    - Service
    - ConfigMap
    - Auth
        - Roles
        - ClusterRoles
        - RolesBindings

Exampl, ingress-wear
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
    name: ingress-wear
spec:
    backend:
        serviceName: wear-service
        servicePort: 80

```

## Ingress Sources Rules
We have rules on the top for each host or domain name, and within each rule we have a different  path to raute traffic based on URL.
How to configure Ingress resources:


### Split traffic by domain name ONE rules

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
    name: ingress-wear-watch
spec:
    rules:
      - http: 
        paths:
        - path: /wear
          backend:
            serviceName: wear-service
            servicePort: 80
        - path: /watch
          backend:
            serviceName: wear-service
            servicePort: 80
```

### Split traffic by domain name TWO rules

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
    name: ingress-wear-watch
spec:
    rules:
    - host:  wear.my-only-store.com
      http:
        - paths:
            - backend:
                serviceName: wear-service
                servicePort: 80
    - host: watch.my-onlie-store.com
      http:
        path:
        - backend :
            serviceName: watch-service
            servicePort: 80
```

```bash
kubectl describe ingress ingress-wear-watch
```


## Ingress
```bash
k get deployments.apps --all-namespaces
k get ingress --all-namespaces
k describe ingress --namespace app-space

kubectl -n app-space describe i ingress-wear-watch
kubectl apply -f ingress.yaml

# Edit or change a yaml
kubectl edit ingress --namespace app-space
kubectl -n app-space get ingress ingress-wear-watch -o yaml > ingress.yaml

k delete ingress ingress-wear-watch -n=app-space
k -n app-space delete ingress ingress-wear-watch
k apply -f /tmp/kubectl-edit-0n15v.yaml
k get services  --all-namespaces
k get deploy  --all-namespaces
k get deployments.app,svc -n critical-space


kubectl get deployments.app, svc -n critical-space
```

# validate Service account

```bash

# Check role and role binding in a Service Account
kubectl get roles,rolebindings -n=ingress-space

kubectl -n ingress-space get roles.rbac.authorization.k8.io
kubectl -n ingress-space get rolebindings.rbac.authorization.k8s.io

kubectl -n app-space describe ingress test-ingress

## Network Polices
kubectl get netpol
kubectl get pods -l name_payroll
kubectl get pods -l name=internal
kubectl describe netpol payroll-policy


```