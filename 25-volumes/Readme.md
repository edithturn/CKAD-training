## Columnes

## Persistent Volumns



PVC =  Persistent Volume Claim 

kubectl get persistentvolumeclaim
kbuectl create -f pvc-definition.yaml



``` Delete PVCs

kubectl delete persistencevolumecaim myclaim

PesistentVolumeReaclaimPolicy: Retain
PesistentVolumeReaclaimPolicy: Delete
PesistentVolumeReaclaimPolicy: Recycle

```
```bash
#logs
kubectl exec webapp -- cat /log/app.log
```


kubectl get pvc
kubectl get pv
k get pv,pvc
k delete pvc claim-log-1