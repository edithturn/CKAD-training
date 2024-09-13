kubectl get pods --all-namespaces | grep <pod-name>
kbuectl get ns | wc -l (answer: total - one)

# Count Containers in a Pod

kubectl get pod red -o jsonpath='{.spec.containers[*].name}' | wc -w

# Look for ht ename

kubectl get pod blue -o jsonpath='{.spec.containers[*].name}'

#

df

k create ingress INGRESSPAY --rule=\*/pay=pay-service:8282

## Roles

k describe role kube-proxy -n kube-system

kubectl create role developer --verb=create --verb=get --verb=delete --resource=pods

kubectl create rolebinding dev-user-binding --role=developer --user=dev-user

ps -ef | grep kube-apiserver | grep admission-plugins

## Grep

# Json

# awk
