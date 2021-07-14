# ConfigMap
ConfigMaps are used to pass configuration data in the form of key value pairs in Kubernetes.

## Creating a ConfigMap

**Imperative**

```bash
#  Create a config map with two  variables, key, value format
kubectl create configmap app-config --from-literal=APP_VERSION=1.0 --from-literal=APP_MODE=dev

# Create a configmap from a file
kubectl create configmap my-config-map --from-file=<path-to-file>

# Create a config map from a properties file
kubectl create configmap app-config --from-file=app_config.properties

# Create a configmap in a specific namespace
kubectl create cm nginx-configuration -n ingress-space

# List configmaps
kubectl get configmaps
```

**Declarative**

my-config-file.yaml
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
	name: app-config
data:
	APP_VERSION: 1.0
	APP_MODE: dev
```
Creating config map from a yaml file
```bash
kubectl create -f my-confg-fle.yaml
kubectl get configmaps
```

## ConfigMap in a Pod (Injection)

pod-definition.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
	name: simple-webapp-color
	labels:
		name: simple-webapp-color
spec:
	containers:
	- name: simple-webapp-color
	image: simple-webapp-color
	ports:
	- containerPort: 808
	envFrom:
		- configMapRef:
			name: app-config
```


