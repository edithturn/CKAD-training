## **Jobs**

```bash
# Job definition
kubectl create -f jobs-definition.yaml

# Imperative commands
kubectl create job pi --image=perl -- perl -Mbignum=bpi -wle 'print bpi(2000)'

# Wait until it is done, get the output
kubectl get jobs -w
# get the name pod
kubectl get po
# Check the logs
kubectl logs pi-rqjqr
# Delete job pi
kubectl delete job pi
```

**Completions**
```bash
# Create a job, make it run 5 times, one after the other. Verify the status and delete it
kubectl create job busybox --image=busybox --dry-run=client -o yaml -- /bin/sh -c 'echo hello;sleep 30;echo world' > job.yaml

# Add the line: completions: 5 , after spec
vim job.yaml

# Create the job
kubectl create -f job.yaml

# Check if this is creating the pods
kubectl get job busybox -w # will take two and a half minutes

# Delete the job
kubectl delete jobs busybox
```
**Completions**
```bash
kubectl create job busybox --image=busybox --dry-run=client -o yaml -- /bin/sh -c 'echo hello;sleep 30;echo world' > job.yaml

# Add this line after spec:   parallelism: 5 # add this line
vi job.yaml

# Create the jobs
kubectl create -f job.yaml

# Check the jobs
kubectl get jobs

# Delete job
kubectl delete job busybox
```


```bash
kubectl get jobs
kubectl get pods
kubectl logs mth-aa-job
kubectl logs 
kubectl delete job mth-aa-job
```

## CronsJobs

```bash
# Create a cron job with image busybox that runs on a schedule of "*/1 * * * *" and writes 'date; echo Hello from the Kubernetes cluster' to standard output
kubectl create cronjob busybox --image=busybox --schedule="*/1 * * * *" -- /bin/sh -c 'date; echo Hello from the Kubernetes cluster'

# See logs and deleted
kubectl get cj
kubectl get jobs --watch
```



## Sources
* The quick and simple editor for cron schedule expressions by Cronitor  https://crontab.guru/examples.html
* https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/#example