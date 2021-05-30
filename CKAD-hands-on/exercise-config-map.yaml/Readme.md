## **Config Maps Problem**
Create a **configMap** called "options" with the value var5=val5. Create a new nginx pod that loads the value from variable 'var5' in an env variable called "option"

## **Solution**
01. Before everything
```bash
alias k=alias
alias kdr='kubectl create --dry-run=client -o yaml'
alias kdp='kubectl delete pod --grace-period=0 --force'
```

02. Now create the config map call "options"
```bash
kubect create cm options --from-literal=var5=val5
```
03. Crate nginx pod yaml and load the value of the variable var5 in an env variable called "option" 
```bash
kdr nginx --image=nginx > pod.yaml
```
04. Edith the pod and add the 'env' section.
Extract from the Kubernetes Documentation [here](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)

```bash
vim pod.yaml
```
```yaml
env:
- name: option
    valueFrom:
        configMapKeyRef:
            name: options
            key: var5
```
05. Create the pod
```bash
k create pod -f pod.yaml
```
06. Finally check the environment variable in the pod
```bash
# It should shows: 'option=val5'
kubectl exec -it nginx -- env  | grep option 
```
