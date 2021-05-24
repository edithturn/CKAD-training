# Hands On

## Exercise 01:

Create a Pod with three busy box containers with commands “ls; sleep 3600;”, “echo Hello World; sleep 3600;” and “echo this is the third container; sleep 3600” respectively and check the status

kubectl run busibox --image=busibox --restart=Never --dry-run -o yaml -- bin/sh -c "sleep 3600; ls" > pod.yml

* Edit the pod after created and add other arguments.

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
```
