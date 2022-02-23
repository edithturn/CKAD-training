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


# Understand Jobs and CronJobs
# Understand multi-container Pod design patterns (e.g. sidecar, init and others)
# Utilize persistent and ephemeral volumes