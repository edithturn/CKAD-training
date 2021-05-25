# Hands On

### Exercise 01:

Create a Pod with three busy box containers with commands “ls; sleep 3600;”, “echo Hello World; sleep 3600;” and “echo this is the third container; sleep 3600” respectively and check the status

**Solution:**

With yml

```yml
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  labels:
    run: busybox
spec:
  containers:
  - args:
    - bin/sh
    - -c
    - ls; sleep 3600
    image: busybox
    name: busybox1
  - args:
    - bin/sh
    - -c
    - echo Hello World; sleep 3600
    image: busybox
    name: busybox2
  - args:
    - bin/sh
    - -c
    - echo this is the third container; sleep 3600
    image: busybox
    name: busybox3
  restartPolicy: Never
  ```

Iterative way: 
```bash
kubectl run busibox --image=busibox --restart=Never --dry-run -o yaml -- bin/sh -c "sleep 3600; ls" > pod.yml
```
* Edit the pod after created and add other arguments for busybox2 and busybox3.

Check the status:

```bash
# Check the logs of each busybox
kubectl logs busibox -c busibox1
kubectl logs busibox -c busibox2
kubectl logs busibox -c busibox3

# Check the previous logs
kubectl logs busibox -c busibox1 --previous
kubectl logs busibox -c busibox2 --previous
kubectl logs busibox -c busibox3 --previous

# Run command ls in a container busybox3
kubectl exec busybox -c busybox3 -- ls
```


### Exercise 02:
Create a Pod with main container busybox and which executes this “while true; do echo ‘Hi I am from Main container’ >> /var/log/index.html; sleep 5; done” and with sidecar container with nginx image which exposes on port 80. Use emptyDir Volume and mount this volume on path /var/log for busybox and on path /usr/share/nginx/html for nginx container. Verify both containers are running.

**Solution:**

With yml

```yml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: multi
  name: multi
spec:
  volumes:
  - name: var-logs
    emptyDir: {}
  containers:
  - image: busybox
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo 'Hi I am from Main container' >> /var/log/index.html; sleep 5;done"]
    name: main-container
    resources: {}
    volumeMounts:
    - name: var-logs
      mountPath: /var/log
  - image: nginx
    name: sidecar-container
    resources: {}
    ports:
      - containerPort: 80
    volumeMounts:
    - name: var-logs
      mountPath: /usr/share/nginx/html  
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

kubectl run multicontainer --image=busybox --restart=Never --dry-run -o yaml > multicontainer.yaml

Edit the yaml and add a second contianer, with volumes

Exec into the containers and verify that main.txt exist and query the main.txt sidecar container with curl localhost

```bash
kubectl exec -it multi -c main-container -- sh cat /var/log/main.txt

kubectl exex -it multi -c sidecar-container -- sh cat /usr/share/nginx/html/index.html

kubectl exec -it multi -c siecar-container -- sh 
# apt-get update && apt-get install -y curl
# curl localhost
```



### Exercise 03:
Create 5 nginx pods in which two of them is labeled env=prod and three of them is labeled env=dev

```bash
kubectl run nginx-dev1 --image=nginx --restart=Never --labels=env=dev
kubectl run nginx-dev2 --image=nginx --restart=Never --labels=env=dev
kubectl run nginx-dev3 --image=nginx --restart=Never --labels=env=dev
kubectl run nginx-prod1 --image=nginx --restart=Never --labels=env=prod

kubectl run nginx-prod1 --image=nginx --restart=Never --labels=env=prod

kubectl get pods --show-labels

# Get the pods with label env=dev
kubectl get pods -l env=dev
kubectl get pods -l env=prod

# Get the pods with label env=dev and show the labels
kubectl get pods -l env=dev --show-labels
kubectl get pods -l env=prod --show-labels

#  Get the pods with label env
kubectl get pod -L env

# Get  the pods with labels env=dev and env=prod
kubectl get pods -l 'env in (dev, prod)'
```
