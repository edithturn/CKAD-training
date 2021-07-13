# Variables in Kubernetes
docker run -e APP_COLOR=pink simple-webapp-color

```bash
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
spec: 
  containers:
  - name: simple-webapp-color
    image: simple-webapp-color
  ports:
    - containerPort: 8080
  env:
    - name: APP_COLOR
      value: pink
```