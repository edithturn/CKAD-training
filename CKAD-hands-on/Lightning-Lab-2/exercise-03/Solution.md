## **Problem**
Create a pod called my-busybox in the dev2406 namespace using the busybox image. The container should be called secret and should sleep for 3600 seconds.

The container should mount a read-only secret volume called secret-volume at the path /etc/secret-volume. The secret being mounted has already been created for you and is called dotfile-secret.

Make sure that the pod is scheduled on master/controlplane and no other node in the cluster.


## **Solution**

```bash
# before this,this is a different namespace, so let set the context ot the namespace

kubectl config set-context --current --namespace=dev2406
# Check in which context are you located, and check the right namespaces

kubectl config get-contexts 
CURRENT   NAME       CLUSTER    AUTHINFO   NAMESPACE
*         minikube   minikube   minikube   dev2406

# Create the pod , we don't need to specify the namespace, we already did in previous steps

kubectl run my-busybox --image=busybox --command sleep 3600 --dry-run -o yaml > busybox.yaml

# Edit the pod yaml and add volumeMounts and secret as a volume, see busybox.yaml
vim busybox.yaml

# add the Node name in the Pod yaml
nodeName: master

# Create the pod
kubectl apply -f busybox.yaml

# Then, check where the pod is running (should be running on Node master)
kubectl get pods  -o wide
```