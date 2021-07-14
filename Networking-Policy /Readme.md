# Networking Policy 

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
kubectl get netpol
kubectl create  -f policy-definition.yaml
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

```bash
Create a temporaly pod to test connection to a pod in a cluster Ip

k get pod -o wide # To get the cluster IP

# To test the conectivity
k run tmp --restart=Never --rm -i --image=nginx:alpine -- curl 10.0.0.67

```

## Network Polices

To allow ingress just in a specific port

```yaml
policyTypes:
- Ingress
ingress:
- from:
    - podSelector:
        matchLabels:
            name: api-pod
  ports:
  - protocol: TCP
    port: 3306  
```
Example of Network Policy

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
    ports:
    - protocol: TCP
      port: 3306
```


## Egress

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
    - Egress
  egress:
  - to:
    - ipBlock:
        cidr: 10.0.0.0/24
    ports:
    - protocol: TCP
      port: 5978

```
