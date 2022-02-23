# Application Design and Build

## Domain & Competencies
* Define, build and modify container images
* Understand Jobs and CronJobs
* Understand multi-container Pod design patterns (e.g. sidecar, init and others)
* Utilize persistent and ephemeral volumes


# Define, build and modify container images
Create and build images, create and run containers. Basic commands:

```bash
# Images
docker images
cat Dockerfile
docker build -t <image-name> .
docker build -t my-app .
docker build -t <image-name>:<image-tag> .
docker build -t my-app:v01 .
# Containers
docker run -p <host-port>:<container-port> <image-name>
docker run -p 8080:8585 my-app
docker ps
docker run <image-name> <command>
docker run my-app cat /etc/*release*
docker run <image-name>:<image-tag> -p <host-port>:<container-port>
docker run my-app:v01 -p 8080:8484
```

### TODO: Docker Architecture, concepts docker and images, dockerflow

# Understand Jobs and CronJobs

## Jobs

Basic Pod definition, is the templete used to create the Job. It executes an addition between two numbers.

```yaml
apiVersion: v1
kind: pod
metadata:
  name: calculator
spec:
  containers:
  - name: math-image
    image: ubuntu
    command: ['expr','4', '+', '5']
```

This job basic-job-template.yaml takes the Pod definition. It will stop when the operation is finished "restartPolicy: Never"
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: calculator
spec:             # spec from Job
  completions: 3  # Each Pod created by the Job controller has an identical spec
  parallelism: 3  # Create parallel Pods instead of sequential ones
  template:
    spec:         # spec from Pod 
      containers:
        - name: math-image
          image: ubuntu
          command: ['expr','4', '+', '5']
      restartPolicy: Never
```
```bash
kubectl create -f basic-job-template.yaml
kubectl get jobs
kubectl logs <name-of-pod>
kubectl logs calculator-ggznd
kubectl delete job calculator
```
## CronJobs

A CronJob creates Job periodically on a given schedule. It takes Job defination. 

basic-cronjob-template.yaml

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: reporting-cron-calculator
spec:                       # spec from CronJob
  schedule: "* * * * *"
  jobTemplate:
    spec:                   # spec from Job
      completions: 3 
      parallelism: 3 
      template:
        spec:               # spec from Pod
          containers:
            - name: math-image
              image: ubuntu
              command: ['expr','4', '+', '5']
          restartPolicy: Never  
```

```bash
kubectl create -f basic-cronjob-template.yaml
kubectl get cj
kubectl get cronjobs
kubectl get pods
kubectl delete cronjobs reporting-cron-calculator
```
### TODO: Dwhat are jobs, cronjobs in kubernetes, template examples

# Understand multi-container Pod design patterns (e.g. sidecar, init and others)


```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-multi-containers
spec:
  restartPolicy: Never
  volumes:
  - name: shared-data
    emptyDir: {}
  containers:
  - name: nginx-container
    image: nginx
    volumeMounts:
    - name: shared-data
      mountPath: /usr/share/nginx/html
  - name: debian-container
    image: debian
    volumeMounts:
    - name: shared-data
      mountPath: /pod-data
    command: ["/bin/sh"]
    args: ["-c", "echo Hello from the debian container > /pod-data/index.html"]
```
## SideCar
Logging service. Deploy login agent.

## Adapter
Processes the logs before sent them to the central server.


## Embassador
Use outsource to separate container within the pod to assign a specific data base.

# Utilize persistent and ephemeral volumes