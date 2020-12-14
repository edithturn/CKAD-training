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

kubectl create secret generic my-scret --from-literal=DB_Host=mysql
--from-literal=DB_User=root
--from-literal=DB_Password=pass
```

```bash
# Declarative
kubectl create -f <secret-file>
```
