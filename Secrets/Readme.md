# Secrets

Secrets to store sensitive information. They are similar to config-maps except that encode the date or hashed format.

There are two steps to implement Secrets:

1. Create a Secret
2. Injected into the pod

## Create a Secret

```console
DB_Host: mariadb
DB_User: root
DB_Password: pass
```

```bash
# Imperative
kubectl create secret generic <secret-name> --from-literal=<key>=<value>

kubectl create secret generic my-secret --from-literal=DB_Host=mysql
--from-literal=DB_User=root
--from-literal=DB_Password=pass

kubectl create secret generic <secret-name> --from-file=<path-to-file>

kubectl create secret generic app-secret --from-file-app_secret.properties


k create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123
secret/db-secret created
```

```bash
# Declarative
kubectl create -f my-secret.yaml
```

This is the structure of a Secret yaml but the data have to be encode (next yaml)

```yaml
apiVersion: c1
kind: Secret
metadata:
  name: app-secret
data:
  DB_Host: mariadb
  DB_User: root
  DB_Password: pass
```

```yaml
apiVersion: c1
kind: Secret
metadata:
  name: app-secret
data:
  DB_Host: bXlzcWw=
  DB_User: cm9vdA==
  DB_Password: cGFzcw==
```

**Creatign secrets | Encode**

```bash
echo -n 'mysql' | base64
bXlzcWw=
```

```bash
echo -n 'root' | base64
cm9vdA==
```

```bash
echo -n 'pass' | base64
cGFzcw==
```

Checking secrets

```bash
kubectl get secrets
kubectl describe secrets
kubectl get secret my-secret -o yaml
```

**Decoding secrets**

```bash
* echo -n 'bXlzcWw=' | base64 --decode
mysql
* echo -n 'cm9vdA==' | base64 --decode
root
* echo -n 'cGFzcw+=' | base64 --decode
pass
```

## Inject into the Pod

**Secret**

```yaml
apiVersion: c1
kind: Secret
metadata:
  name: app-secret
data:
  DB_Host: bXlzcWw=
  DB_User: cm9vdA==
  DB_Password: cGFzcw==
```

**Secret in Pod**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-web
  labels:
    name: app-web
spec:
  containers:
    - name: app-web
      image: app-web
      port:
        - containerPort: 8080
      envFrom:
        - secretRef:
            name: app-secret
```

### TODO

- Secrets kubernetes

* Helm Secrets
* HashiCorp Vault
