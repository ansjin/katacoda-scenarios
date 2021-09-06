#### Copy kube config file
`mkdir -p $HOME/.kube`{{execute HOST1}}

`sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config`{{execute HOST1}}

`sudo chown $(id -u):$(id -g) $HOME/.kube/config`{{execute HOST1}}

#### Health Check

Once started, you can get the status of the cluster with `kubectl cluster-info`{{execute}}

To be sure you have at least one worker node. If you see only master node in the katacode then restart it. (refresh page)
`kubectl get nodes`{{execute}}

Output:


| NAME        | STATUS           | ROLES  |  AGE | VERSION|
| ------------- |:-------------:| -----:|-----:|-----:|
| controlplane     | NotReady | master| 13m| v1.18.0|

#### Taint master node.

`kubectl taint nodes --all node-role.kubernetes.io/master-`{{execute HOST1}}

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


#### Health Check

Again now do the health check . 

`kubectl get nodes`{{execute}}

Output:


| NAME        | STATUS           | ROLES  |  AGE | VERSION|
| ------------- |:-------------:| -----:|-----:|-----:|
| controlplane     | Ready | master| 13m| v1.18.0|