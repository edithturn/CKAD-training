# **Pod multi container**

```bash
# Create the pod with a contianer
kubectl --dry-run=client -o yaml busybox --image=busybox --  /bin/bash  -c "ls; sleep 3600" > multi-container.yaml

# Edit the pod to add more container
vim multi-container.yaml
```

```bash
# See the logs of cotainer busybox1
$ kubectl logs busybox -c busybox1
bin
dev
etc
home
proc
root
sys
tmp
usr
var
```
```bash
# See the logs of cotainer busybox2
kubectl logs busybox -c busybox2
```
```console
$ Hello World
```
```bash
# See the logs of cotainer busybox3
kubectl logs busybox -c busybox3
```
```console
$ this is the third container
```
```bash
# Run commands ls in the third  container busybox3
kubectl exec busybox -c busybox -- ls
```
