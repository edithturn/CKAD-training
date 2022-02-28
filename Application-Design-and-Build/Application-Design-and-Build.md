# Application Design and Build

## Domain & Competencies
* Define, build and modify container images
* Understand Jobs and CronJobs
* Understand multi-container Pod design patterns (e.g. sidecar, init and others)
* Utilize persistent and ephemeral volumes


# Define, build and modify container images
Create and build images, create and run containers. Basic commands:

## What is Docker?

Docker is an open source technology for building, deploying, and managing containerized applications. Docker Architecture:

<p align="center">
  <img width="600" height="320" src="../img/docker-architecture.png">
</p>

[Source docs.docker.com](https://docs.docker.com/get-started/overview/)

## Images and Containers

Docker images are templates used to build containers. Containers are application in execution (alive), product of build docker images.  There are three main elements to create containers:



<p align="center">
  <img width="600" height="320" src="../img/dockerfile-image-container.png">
</p>

[Source Nilesh Jayanandana](https://medium.com/platformer-blog/practical-guide-on-writing-a-dockerfile-for-your-application-89376f88b3b5)

## Basic Commands

Images
```bash
# Images
docker images
cat Dockerfile
docker build -t <image-name> .
docker build -t my-app .
docker build -t <image-name>:<image-tag> .
docker build -t my-app:v01 .
```
Containers
```bash
docker run -p <host-port>:<container-port> <image-name>
docker run -p 8080:8585 my-app
docker ps
docker run <image-name> <command>
docker run my-app cat /etc/*release*
docker run <image-name>:<image-tag> -p <host-port>:<container-port>
docker run my-app:v01 -p 8080:8484
```

# Understand Jobs and CronJobs

## What is a Job?

A job creates one or more pods and will continue to retry the pods until it successfully completes the number of pods defined in the Job. A Job needs a Pod definition for its creation.

Let's see this Pod Defination, which purpose is add two numbers.

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

basic-job-template.yaml It is a Job that will take the previous Pod definition and, It will stop when the operation is finished "restartPolicy: Never"

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

Jobs

```bash
kubectl create -f basic-job-template.yaml
kubectl get jobs
kubectl logs <name-of-pod>
kubectl logs calculator-ggznd
kubectl delete job calculator
```
## CronJobs

Cron is a time-based job scheduler in Linux and Unix systems. 

<p align="center">
  <img width="600" height="320" src="../img/cron.png">
</p>

Use [crontab.guru](https://crontab.guru/) to practice cron schedule expressions.

A CronJob creates Job periodically on a given schedule. It takes a Job defination. For example:

basic-cronjob-template.yaml

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: reporting-cron-calculator
spec:                       # CronJob spec
  schedule: "* * * * *"
  jobTemplate:
    spec:                   # Job spec
      completions: 3 
      parallelism: 3 
      template:
        spec:               # Pod spec
          containers:
            - name: math-image
              image: ubuntu
              command: ['expr','4', '+', '5']
          restartPolicy: Never  
```

## Basic Commands

CronJobs

```bash
kubectl create -f basic-cronjob-template.yaml
kubectl get cj
kubectl get cronjobs
kubectl get pods
kubectl delete cronjobs reporting-cron-calculator
```

# Multi-Containers

## TODO: Understand multi-container Pod design patterns (e.g. sidecar, init and others)


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