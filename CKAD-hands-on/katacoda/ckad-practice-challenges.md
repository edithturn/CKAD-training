# katacoda - CKAD Practice Challenge

Link to practice [HERE](https://www.katacoda.com/liptanbiswas/courses/ckad-practice-challenges)


<p align="center">
  <img width="500" height="350" src="../../img/katakoda.png">
</p>


# Exercises

# asdas

## Exercise 03:
Create a service messaging-service to expose the redis deployment in the marketing namespace within on port 6379

**Solution:**
```bash
# Set the context in the current namespace
kubect config set-context --current --namespace=marketing
# Create the service with expose and add the ports
kubectl expose deploy redis messaging-service -n masrketing --port 6379 --targetPort 6379
```

## Exercise 04:
Find the name of pod which is using most CPU across all namespaces. Enter the name of pod in /root/high-cpu.yaml

```bash
kbuectl top po -A --sort-by=cpu
```

### Exercise 05:

Deployment naboo is created. Make sure the replicas autoscale with minimum 2 and maximum 5 when at 80% CPU. Use naboo as the name of HPA resource.

```bash
kubectl autoscale deploy naboo --name=naboo --min=2 --max=5 --cpu-percent=80
```


### Exercise 06:
Create a Cron job bespin that runs every 5 minutes(*/5 * * * *) and runs command date. Use alpine image.

```bash
kubectl create cronjob bespin --image=alpine --schedule="*/5 * * * *" -- date
```



# Services & Networking - 13%
## Question 01
Create a pod named ig-11 with image nginx and expose its port 80.

Solution:

```bash
k run ig-11  --restart=Never --image=nginx --port=80
```
## Quesion 02
Create a service for pod ig-11 on using ClusterIP type service with service name greef. Map service port 8080 to container port 80.

Solution:

```bash
k expose pod ig-11 --name=greef --port=8080 --target-port=80
```

## Quesion 03

Deployment cara is created. Expose port 80 of the deployment using NodePort on port 31888. Use cara as service name.

Solution:
```bash
k expose deployment cara --port=80 --type=NodePort

#  k edit service cara
# then change nodePort to 31888
```

## question 4
Pod and Service geonosis is created for you. Create a network policy geonosis-shield which allows only pods with label empire=true to access the service. Use appropriate labels.

Solution:

```bash
vim np.yaml
```
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: geonosis-shield
  namespace: default
spec:
  podSelector:
    matchLabels:
      sector: arkanis # Take the labels of the service and of the pod
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          empire: "true"
```

# State Persistence - 8%

## Question 01

Create a pod named "tato" with image nginx. Mount a volume named tato-vol at /var/www/html, which should live as long as pod lives.

**Solution**
```bash
alias kdr='kubectl run --dry-run -o 
yaml'
kdr tato --image=nginx > pod.yaml
```
vim pod.yaml
```yaml
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: tato
  name: tato
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
    volumeMounts:
    - mountPath: /var/www/html
      name: tato-vol
  volumes:
  - name: tato-vol
    emptyDir: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

## Question 02

Create a persistent volume "first-pv" with 100Mi at /data/mysql on host. Use manual storageClassName and ReadWriteMany access mode.

Create a persistent volume claim "first-pvc" and consume the pv first-pv.

Create a pod "magic" with image mysql and mount the PVC at /var/lib/mysql using volume name first-vol. Set an environment variable MYSQL_ROOT_PASSWORD=my-secret-pw as well.

**Solution**

vim pv.yaml
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: first-pv
spec:
  capacity:
    storage: 100Mi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: manual
  hostPath:
    path: /data/mysql
```
vim pvc.yaml
```yaml
kind: PersistentVolumeClaim
metadata:
  name: first-pvc
spec:
  accessModes:
    - ReadWriteMany
  volumeMode: Filesystem
  resources:
    requests:
      storage: 100Mi
  storageClassName: manual
```
kubectl run magic --image=mysql > pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: magic
  name: magic
spec:
  containers:
  - image: mysql
    name: mysql
    env:
    - name: MYSQL_ROOT_PASSWORD
      value: "my-secret-pw"
    resources: {}
    volumeMounts:
      - mountPath: "/var/lib/mysql"
        name: first-vol
  volumes:
    - name: first-vol
      persistentVolumeClaim:
        claimName: first-pvc
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```


## Question 03
Create a pod "moodo" with two containers using image nginx and redis. Create a shared hostPath volume at /data/moodo named moodo-logs mounted at /var/log/moodo in both the containers.

**Solution**

vim pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: moodo
  name: moodo
spec:
  containers:
  - image: nginx
    name: nginx
    volumeMounts:
    - mountPath: /var/log/moodo
      name: moodo-logs
  - image: redis
    name: redis
    volumeMounts:
    - mountPath: /var/log/moodo
      name: moodo-logs
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  volumes:
  - name: moodo-logs
    hostPath:
      path: /data/moodo
status: {}
```