# ConfigMap
ConfigMaps are used to pass configuration data in the form of key value pairs in Kubernetes.

## Creating a ConfgMap

ConfigMap
```console
APP_VERSION: 1.0
APP_MODE: dev
```

```bash
kubectl create configmap <config-name> --from-literal=<key>=<value>

kubectl create configmap app-config  app-config --from-literal=APP_VERSION=1.0 --from-literal=APP_MODE=dev

kubectl create configmap my-config-map --from-file=<path-to-file>

kubectl create configmap app-config --from-file=app_config.properties

kubectl create cm nginx-configuration -n ingress-space
```

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


