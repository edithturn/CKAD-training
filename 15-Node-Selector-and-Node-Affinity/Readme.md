## **Node Selector**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: test
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  nodeSelector:   # Deploy pod in nodes with ssd disk type
    disktype: ssd
```

## **Node Affinity**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disktype  # Size    # Size
            operator: In   # NotIn   # Exists
            values:    
            - ssd          # Small 
            - hd           # Medium
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
```