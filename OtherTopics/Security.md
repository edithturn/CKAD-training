# Security at kube-apiserver

Who can access?

- fils user admins and passwords
- Files user names and tokens
- Crtificates
- LDAP
- Service accounts

What they can do?

- RBAC authorization
- ABAC
- Node authorization
- Webhook mode

Kube ApiServer is secure with TLS Certificates

- ETD Cluster
- kubelet
- kube proxy
- kube control manager
- kube scheeduler

By default all pods can access all pods into the cluster. It is posible to restrict access using Network Polices.

## Authentication

- Admins and Developers -> It is NOT possible manage it with Kubernetes
- Boots -> Service Account It is possible to create to manage these users

## Admins and Developers

All user accss is manage with kube-apiserver.
The kube-api server autenticates before the request before processing.

## Kubeconfig

- Clusters
- Contexts: match user and clusters
- Users

```bash
kubectl config use-context prod-user@production
```

cat ca.crt| base64

## API Groups

curl http://localhost:6443 -k
curl http://localhost:6443/apis -k | grep "name"

kube proxy =! kubectl proxy

## RBAC

```bash
#existig rolebinding
kubectl describe rolebinding devuser-developer-binding
```

```bash
kubeck auth can -i create deployment
kubecl auth can -i delete nodes

kubecl auth can-i create deployments --ass dev-user

kubec auth can-i crate pods --as dev-user
kubectl auth can-i crate pods --as dev-user --namespace test

```

## Cluster Roles

## Admision Controlers

```bash
kube-apiserver -h | grep enable-admission-plugins
```
