kubectl get pods --all-namespaces | grep <pod-name>
kbuectl get ns | wc -l (answer: total - one)

# Count Containers in a Pod

kubectl get pod red -o jsonpath='{.spec.containers[*].name}' | wc -w

# Look for ht ename

kubectl get pod blue -o jsonpath='{.spec.containers[*].name}'

#

df

k create ingress INGRESSPAY --rule=\*/pay=pay-service:8282

## Roles

k describe role kube-proxy -n kube-system

kubectl create role developer --verb=create --verb=get --verb=delete --resource=pods

kubectl create rolebinding dev-user-binding --role=developer --user=dev-user

ps -ef | grep kube-apiserver | grep admission-plugins

## Grep

# Json

# awk

kubectl exec james -- printenv | grep FRONT_ROW
kubectl get pods --selectors env=dev --no-headers | wc -l

## GREP

```bash
#  Total count of pods with the label env=dev, excluding the header.
kubectl get pods --show-labels | grep -c 'env=dev'

#  Total count of objects with the label env=prod, excluding the header.
k get all  --show-labels | grep '-c'  env=prod

#  Total count of objects with diferent labels
k get pod --show-labels | grep env=prod | grep bu=finance | grep tier=frontend

```

## Tips and Tricks for AWK and Grep

### Using grep and awk to Extract Pod Information

```bash
$ k get pod -owide
NAME    READY   STATUS    RESTARTS   AGE     IP            NODE     NOMINATED NODE   READINESS GATES
mypod   1/1     Running   0          2m56s   192.168.1.6   node01   <none>           <none>
nginx   1/1     Running   0          5m23s   192.168.1.4   node01   <none>           <none>
$ k get pod -owide | awk '{ print $1, $6 }'
NAME IP
mypod 192.168.1.6
nginx 192.168.1.4
```

### Extract Specific Values from Pod Descriptions

Filter Pods by Status

```bash
# To find all pods that are not in the "Running" status:
$ k get pod | grep -v "Running"
NAME       READY   STATUS         RESTARTS   AGE
fail-pod   0/1     ErrImagePull   0          14s
# To find all pods that are in the "Running" status:
controlplane $ k get pod | grep "Running"
mypod      1/1     Running            0          9m48s
nginx      1/1     Running            0          12m
```

Extract Specific Values from Pod Descriptions

```bash
$ k describe pod mypod | grep "Node:"
Node:             node01/172.30.2.2

$ k describe pod mypod | grep "Node:" | awk '{print $2}'
node01/172.30.2.2
```

Get the Container Image in a Pod

```bash
k get pod nginx -ojsonpath='{.spec.containers[*].image}'
nginx

$ k describe pod nginx | grep "Image:"
    Image:          nginx
$ k describe pod nginx | grep "Image:" | awk '{print $2}'
nginx
```

### Resource Requests and Limits

```bash
# -A 2: This option tells grep to print 2 lines after the matching line.
# For Limits
$ k describe  pod nginx | grep -A 2 "Limits" | awk '{print $1, $2}'
Limits:
cpu: 500m
memory: 128Mi

# For Requests
$ k describe  pod nginx | grep -A 2 "Request" | awk '{print $1, $2}'
Requests:
cpu: 250m
memory: 64Mi
```

### Filtering Events for Troubleshooting

```bash
# Searches for lines containing "Warning" and displays the match along with the next 5 lines for each match.
$ kubectl describe pod mypod | grep -A 5 "Warning"
```

### Service and Endpoint Information

Get the Cluster IP of a Service

```bash
# With jsonpath
$ k get svc nginx -o jsonpath='{.spec.clusterIP}'
10.97.243.240

# With Grep and AWK
$ kubectl describe svc mypod | grep "NodePort" | awk '{print $3}'
30288/TCP
```

Count and List Pods by Labels

```bash
# Count Pods with a Specific Label

k get pods --show-labels
NAME    READY   STATUS    RESTARTS   AGE   LABELS
nginx   1/1     Running   0          27s   run=nginx
# wc -l is a Linux command that counts the number of lines in the output it receives.
k get pods -l run=nginx --no-headers | wc -l
1


# List Pod Names with a Specific Label
$ k get pods -l run=nginx  -o custom-columns=":metadata.name"
nginx
```

### Extract and Format Timestamps of Pod Events

```bash
k get pod nginx -o jsonpath='{.status.startTime}'
2024-11-11T18:20:14Z
```

### Custom Column Outputs for Readability

```bash
k get pods -o custom-columns="POD:metadata.name,STATUS:status.phase"
POD     STATUS
nginx   Running
```

```bash
# For each line, it would print the first field (typically the username):
cat /etc/passwd | awk -F ":" '{print $1}'
```
