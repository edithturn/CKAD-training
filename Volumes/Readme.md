# State Persistence

## Volumes

The data that is on the container lives with the container, It means that if the container died the data is destroyed.
To persit the date, we have to attach a volumne in the container to retain permanently.

**Example**
  - In volumes, firt we need to create the volume call it: data-volume, then the hostPath where we will store the data
  - In container section, we mount the data-volume in a container directory /opt
  - If the pod is deleted the file /data still on the host

```bash
kubect create -f pod-definition.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: random-number-generator
spec:
  containers:
  - name: alpine
    image: alpine
    command: ["/bin/sh", "-c"]
    args: ["shuf -i 0-100 -n 1 >> /opt/number.out;"]
    volumeMounts:
    - mountPath: /opt
      name: data-volume
  volumes:
    - name: data-volume
      hostPath:
        path: /data
        type: Directory
```

## Persistent Volumes  - PV
A persistent volume is a cluster wide pool of storage volumes configured by an administrator to be used. The users can select storage from this pool using Persisten Volume claims.

Note:
AccessModes support:
- ReadOnlyMany
- ReadWriteOnce
- ReadWriteMany

```bash
kubectl create -f pv-definition.yaml
kubectl get persistentvolume
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-vo11
spec:
  accessModes:
    - ReadWriteOnde
  capacity:
    storage: 1Gi
  hostPath:
    path: /data
```

## Persistent Volumns Claims - PVC
Persistent volumes and persisten volume claims are separate objects in Kubernetes namespaces. An administrator create a persistent volumes and an user create a persisten volume claims to use storage.

Kubernetes binds the Persisten Volumes to Claims based. Every persistent Volume Claim is bound to a single Persistent Volume.

```bash
kubectl create -f pvc-definition.yaml
kubectl get persistentvolumeclaim
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests: 
      storage: 500Mi
```

Note: The Persistent Volume Claim after creation will be on Pending status,  when claim is created Kubernetes looks for a "volume" created previously, if the accessModes match, the capacity is less thatn Persistent Volume, since there are not other who match with the claim requierement, the persistent volume claim will be bound to the persisten volume. 

```bash
kubectl get persistentvolumeclaim
kbuectl create -f pvc-definition.yaml
```

### Deleting PVCs

```bash
kubectl delete persistencevolumeclaim myclaim

# We can choose what do with the volume,, by default is Retain
PesistentVolumeReaclaimPolicy: Retain  # The persistent volume will remain until it is deleted manually by the administrator, is not available for other claims
PesistentVolumeReaclaimPolicy: Delete # Delete automatically, if the claim is deleted the volume will be deleted too
PesistentVolumeReaclaimPolicy: Recycle # The data in the data volume will be scrubbed before making it availabe to other claims

```

## Using PVCs in PODs
In the pod we are using the Persistent Claim that we already created "myclaim" as a volume. Then mount that volumen in the container.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: myclaim
```

```bash
#logs
kubectl exec webapp -- cat /log/app.log
```


### Other commands
```bash
kubectl get pvc
kubectl get pv
k get pv,pvc
k delete pvc claim-log-1
```