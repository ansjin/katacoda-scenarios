#### Copy kube config file
`mkdir -p $PWD/.kube`{{execute HOST1}}
`sudo cp /etc/kubernetes/admin.conf $PWD/.kube/config`{{execute HOST1}}


#### Taint master node.

`kubectl taint node-role.kubernetes.io/master-`{{execute HOST1}}

#### Install Kubernetes CNI plugin

We are creating flannel CNI
`kubectl apply -f assets/flannel.yml`{{execute HOST1}}

Wait for the pods to get ready, check the status uing the command: 
`kubectl get pods --all-namespaces`{{execute}}

Output:


| NAMESPACE        | NAME           | READY  |  STATUS | RESTARTS | AGE|
| ------------- |:------------------------------------------:| -----:|-----------:|-----:|-----:|
| kube-system     | coredns-558bd4d5db-8mhkr | 1/1| Running| 0 | 15m|
| kube-system     | etcd-fraphisprk00033  | 1/1| Running| 0 | 15m|
| kube-system     | kube-apiserver-fraphisprk00033  | 1/1| Running| 0 | 15m|
| kube-system     | kube-proxy-92zkf  | 1/1| Running| 0 | 15m|
| kube-system     | kube-proxy-92zkf  | 1/1| Running| 0 | 15m|
| kube-system     | kube-scheduler-fraphisprk00033  | 1/1| Running| 0 | 15m|
| kube-system     | kube-controller-manager-fraphisprk00033  | 1/1| Running| 0 | 15m|