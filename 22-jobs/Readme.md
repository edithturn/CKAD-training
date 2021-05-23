## Jobs

``bash
kubectl create -f jobs-definition.ymal
kubectl get jobs
```

kubectl get jobs
kubectl get pods
k logs mth-aa-job
kubectl logs 
kubectl delete job mth-aa-job
```

k describe job throw-dice-pod.yaml throw-dice-job
kubectl create job throw-dice-job --image kudekloud/throw-dice --dry-run=client -o yaml > job.yaml 

kubectl create job 

**watch**
watch "kubectl get job"


## Crons

kubectl create cronjob throw-dice-dron=job --image kodecloud/throw-dice --schedule "30 21  * * *" --dry-run=client -o yaml >c cronjob.yaml

kubectl get cronjobs.batch throw-dice-cron-job
