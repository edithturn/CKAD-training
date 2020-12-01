# Troubleshooting

## 
If you are working in GPC with Docker, you could have this error message when you restart the cluster
```bash
edith@master:~$ kubectl get pods
The connection to the server localhost:8080 was refused - did you specify the right host or port?
```
Solution
```bash
 mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```