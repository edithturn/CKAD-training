# Hands On -- More Practice

In this folder I sumarized some points of the tests that I took before the exam.

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

Imperative: 
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
kubectl get pods -l 'env in (dev, prod)'\

# Get the pods with labelsenv=dev and env=prod and output the labels as well
kubectl get pods -l 'env in (dev, prod)' --show-labels

# Change the label of one of the pod to env=uat and list all the pods to verify
kubectl label pod/nginx-dev3 env=uat --overwrite

# Remove the labels for the pods that we created now and verify all the labels are removed
kubectl label pod nginx-dev{1..3} env-

# Label the node nodename=nginxnode
kubectl label node monikube 

# Label thenode (minikube) nodeName=nginxnode
kubectl label node minikube nodeName=nginxnode

# Create a pod that will be deployed on this node with the label nodeName=nginx
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > pod.yaml

# Edit the pod an add the nodeSelectos, then create it
kubectl create -f pod.yaml

# Verify the pod that it is scheduled with the node selectos
kubectl describe po nginx | grep Node-Selectors

# Verify the pod nginx that we just created has this label
kubectl describe po nginx | grep Labels

# Annotate the pods with name=webapp
kubectl annotate pod nginx{1..2} name=webapp
kubectl annotate pod nginx-prod{1..2} name=webapp

# Verify the pods that have been annotated 
kubectl describe po nginx-dev{1..3} | grep -i annotations
kubectl describe po nginx-pro{1..2} | grep -i annotations

# Remove the annotations of the pod and verify
kubectl annotate pod nginx-dev{1..3} name-
kubectl annotate pod nginx-prod{1..2} name-

# checking if they have annotations
kubectl describe po nginx-dev{1..3} | grep -i annotations
kubectl describe po nginx-prod{1..2} | grep -i annotations
```


