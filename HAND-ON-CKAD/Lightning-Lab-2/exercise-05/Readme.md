## **Problem**

A pod called dev-pod-dind-878516 has been deployed in the default namespace. Inspect the logs for the container called log-x and redirect the warnings to /opt/dind-878516_logs.txt on the master node

## **Solution**


```bash
# Check the pod and their containers
kubectl describe pod dev-pod-dind-878516

# Check the container log-x and their logs with WARN message, the redirect it to /opt/dind-878516_logs.txt on master note
kubectl logs  dev-pod-dind-878516 -c log-x | grep WARN > /opt/dind-878516_logs.txt

# Check the file is saving the logs of the container
cat /opt/dind-878516_logs.txt

```