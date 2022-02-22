## **Problem**
Create a cronjob called dice that runs every one minute. 
Use the Pod template located at /root/throw-a-dice. 
The image throw-dice randomly returns a value between 1 and 6. 
The result of 6 is considered success and all others are failure.
The job should be non-parallel and complete the task once. Use a backoffLimit of 25.
If the task is not completed within 20 seconds the job should fail and pods should be terminated.

You don't have to wait for the job completion. As long as the cronjob has been created as per the requirements.

## **Solution**

```bash
# Check the Pod definition file, and get the Pod name to create the cronJob
cat throw-dice-pod

# Create the Cron Job
kubectl create cronjob dice --image=kodekloud/throw-dice --schedule "* * * * *" --dry-run=client -o yaml > dice.yaml

# Edit the CronJob file and add these lines
vim dice.yaml
```
```yaml
    backoffLimit: 25
    completions: 5
    activeDeadlineSeconds: 100
```

```bash
# Create the CronJob
kubectl create  -f dice.yaml

# Check if the jobs are running
kubectl get jobs

```