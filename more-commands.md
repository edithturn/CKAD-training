# Tips and Tricks

These are some extra commands you might find useful. They are more specific, so I added them to this new sheet of tips and tricks. I hope they help make your work easier. Don’t forget to practice them to get better at using these tools!

Work In Progress 🚜 🛠️ 🚧

> Note: I will keep updating this document with more tips and tricks.

## 📙️ Help

Use the power of `help`.
Which provides help documentation and usage details (syntax, flags, and options available) for the specific command. Also Offers examples of usage.

Example:

Running `kubectl run --help` might give you information like:

```bash
Create and run a particular image in a pod on the cluster.

Examples:
  # Start a single instance of nginx.
  kubectl run nginx --image=nginx

Options:
  --image: The container image to use.
  --port: The port to expose on the pod.
  ...
```

## 📗 Explain

Use the power of `explain` which provides schema information about a specific Kubernetes resource, including its fields and structure. It also helps you understand the API definition for the resource and how to configure it in YAML or JSON.

Example:

Running `kubectl explain pod` might give you information like:

```bash
KIND:     Pod
VERSION:  v1

DESCRIPTION:
     Pod is a collection of containers that can run on a host. This resource is created by clients and scheduled onto hosts.

FIELDS:
     apiVersion  <string>
       APIVersion defines the versioned schema of this representation of an object. Servers should convert recognized schemas to the latest internal value, and may reject unrecognized values.
     kind  <string>
       Kind is a string value representing the REST resource this object represents.
```

## When to use `help` or `explain`?

Use `--help` to understand how to execute a command.
Use `kubectl explain` to understand how a Kubernetes resource is defined and structured.

```bash
kubectl get pods --all-namespaces | grep <pod-name>
kbuectl get ns | wc -l (answer: total - one)
```

## Counting containers in a pod

```bash
kubectl get pod mypod -o jsonpath='{.spec.containers[*].name}' | wc -w
```

## Print the name of the containers in the pod named 'mypod'

```bash
kubectl get pod mypod -o jsonpath='{.spec.containers[*].name}'
```

## Roles

```bash
# Describe the role named 'kube-proxy' in the 'kube-system' namespace.
k describe role kube-proxy -n kube-system

# Create a role named 'developer' with the following permissions:
kubectl create role developer --verb=create --verb=get --verb=delete --resource=pods

# Create a rolebinding named 'dev-user-binding' that binds the role 'developer' to the user 'dev-user
kubectl create rolebinding dev-user-binding --role=developer --user=dev-user

# Checks if the kube-apiserver is running and whether it has admission plugins enabled
ps -ef | grep kube-apiserver | grep admission-plugins
```

## Grep, awk and jsonpath

```bash
# Print all environment variables in the pod named 'james'
kubectl exec james -- printenv | grep FRONT_ROW

# Counts the number of pods in the dev environment
kubectl get pods --selectors env=dev --no-headers | wc -l
```

```bash
# Shows pod details and highlights the annotations: section with 10 lines before and after it.
kubectl describe pods | grep --context=10 annotations:

# Shows pod details and highlights the Events: section with 10 lines before and after it.
kubectl describe pods | grep --context=10 Events:

#  Total count of pods with the label env=dev, excluding the header.
kubectl get pods --show-labels | grep -c 'env=dev'

#  Total count of objects with the label env=prod, excluding the header.
k get all  --show-labels | grep '-c'  env=prod

#  Total count of objects with diferent labels
k get pod --show-labels | grep env=prod | grep bu=finance | grep tier=frontend

# lists all deployments in all namespaces (-A) in a detailed format (-o wide) and filters by image.
k get deployments.apps -A -o wide | grep kodekloud/webapp-color:v1
```

### Using grep and awk to Extract Pod Information

```bash
# Lists all pods in the current namespace with additional details
$ k get pod -owide
NAME    READY   STATUS    RESTARTS   AGE     IP            NODE     NOMINATED NODE   READINESS GATES
mypod   1/1     Running   0          2m56s   192.168.1.6   node01   <none>           <none>
nginx   1/1     Running   0          5m23s   192.168.1.4   node01   <none>           <none>

# Extract the Pod Name and IP Address
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

### Extract Specific Values from Pod Descriptions

```bash
# Retrieves details of the pod named and filters to show the line containing the Node: information
k describe pod mypod | grep "Node:"
Node:             node01/172.30.2.2

# Extracts the Node name from the output
$ k describe pod mypod | grep "Node:" | awk '{print $2}'
node01/172.30.2.2
```

```bash
# Get the container image in a pod using jsonpath
k get pod nginx -ojsonpath='{.spec.containers[*].image}'
nginx

# Retrieves details of the nginx pod and filters by the line containing Image:
k describe pod nginx | grep "Image:"
    Image:          nginx

# Retrieves the image name used by the nginx pod. It filters the Image: line and uses awk to extract and print the second column
k describe pod nginx | grep "Image:" | awk '{print $2}'
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

# Output to a file
kubectl logs nginx | sudo tee ~/opt/answers/nginx.logs
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

## Decode a Base64 string

To Encode:

```bash
echo -n "your_word" | base64
```

To Decode:

```bash
echo -n "your_base64_string" | base64 --decode

```

## How to Test Things

### When to Choose Which in Kubernetes?

- Use curl for:

API interaction or testing HTTP responses (GET, POST, PUT, DELETE).
Debugging advanced HTTP headers or response status.
Validating DNS resolution with specific request formats.

Examples:

```bash
# Test Connectivity to a Pod or Service. In this case validate if a service named my-service running on port 8080 is accessible.
kubectl run tmp --image=busybox --rm -i -- curl -m 5 http://my-service:8080

# Check the Headers or Debug Responses. Here validate the HTTP headers returned by a service to debug load balancer configurations or caching.
kubectl run tmp --image=busybox --rm -i -- curl -I http://my-service:8080

# Fetch Cluster DNS Resolution. Ensure DNS resolves a specific pod or service correctly within the cluster.
kubectl run tmp --image=busybox --rm -i -- curl -m 5 http://my-pod.my-namespace.svc.cluster.local

```

- Use wget for:

Simple connectivity checks (e.g., "Is this service reachable?").
Downloading files (e.g., downloading a binary or a script for setup).

Examples:

```bash

# Test Connectivity to a Pod or Service or Basic DNS and Service Testing. Similar to the curl example but focuses on retrieving content quickly.
kubectl run tmp --image=busybox --rm -i -- wget -O- -T 5 http://my-service:8080

# Download a File. Retrieve and save a file from an external URL for use in your container.
kubectl run tmp --image=busybox --rm -i -- wget -O myfile.txt http://example.com/file.txt
```

### Test network polices

```bash

k -n space1 exec app1-0 -- curl -m 1 microservice1.space2.svc.cluster.local

k -n space1 exec app1-0 -- nslookup tester.default.svc.cluster.local
```

## Test svc

```bash
k run test --image=nginx --rm -n ckad12-svcn -it -- sh
k run test --image=nginx --rm -it -- sh
```

## helm

```bash
helm install kubernetes-dashboard-server kubernetes-dashboard/kubernetes-dashboard -n cd-tool-apd

```
