## ConfigMaps


** Imperative
```bash
kubectl create configmap
```

** Declarative
```bash
# Creating with a file defination
kubectl create -f

# Passing parameters
kubectl create configmap \
app-config --from-literal=APP_COLOR=blue \
--from-lteral=APP_MOD=prod

# Create configmap with a file
kubectl create configmap app-config --from-fil=app_config.properties

```
