# katacoda - CKAD Practice Challenge

Link to practice [HERE](https://www.katacoda.com/liptanbiswas/courses/ckad-practice-challenges)


<p align="center">
  <img width="500" height="350" src="../../img/katakoda.png">
</p>


# Exercises

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



# Services & Networking
## Question 01
Create a pod named ig-11 with image nginx and expose its port 80.

Solution:
```bash
k run ig-11 --image=nginx --port=80
```
## Quesion 02
Create a service for pod ig-11 on using ClusterIP type service with service name greef. Map service port 8080 to container port 80.

k expose pod ig-11 --name=greef --port=8080 --target-port=80


## Quesion 03

Deployment cara is created. Expose port 80 of the deployment using NodePort on port 31888. Use cara as service name.

k expose deployment cara --port=80 --type=NodePort

k edit service cara
then change nodePort to 31888

## question 4
Pod and Service geonosis is created for you. Create a network policy geonosis-shield which allows only pods with label empire=true to access the service. Use appropriate labels.


apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: geonosis-shield
spec:
  podSelector:
    matchLabels:
      sector: arkanis
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          empire: "true"                               