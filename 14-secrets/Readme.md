## Secrets

```bash
kubectl create secretr generic <secret-name> --from-literal=<key>=<value>

kubect create secret generic app-secret --from-literal=DB_Host=mysql


kubectl crate secret generic app-secret --from-file=app_secret.properties
```

```bash
kubectl get secrets
kubectl describe secret

# Get the configurarion of a secret in to a file
kubectl get secret app-secret -o yaml
```


**Creatign secrets | Encode**
```bash
echo -n 'mysql' | base64
echo -n 'root' | base64
echo -n 'passwrd' | base64
```

**Decoding secrets**

``bash
echo -n 'asdasdas=' | base64 --decode
mysql

echo -n 'cmdsahdA=='  | base64 --decode
root

echo -n 'Getafaf' | base64 --decode
passwd
```



