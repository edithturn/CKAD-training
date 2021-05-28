
## Network in Kubernentes
* routing


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
Then:
```bash
kubectl create  -f policy-definition.yaml
```

```bash
kubectl get netpol
```
