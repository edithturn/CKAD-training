## Solution

Check the template
```bash
cat throw-dice-pod

# Create the Cron Job
kubectl create cronjob dice --image=kodekloud/throw-dice --schedule "*/1 * * * *" --dry-run=client -o yaml > dice.yaml

# Edit the Cron Job file
vim dice.yaml
```

```bash
kubectl create  -f dice.yaml
```


```bash

```
