Since in our cluster master node will also run application pods therefore we need to taint it.

#### Taint master node.

`kubectl taint nodes --all node-role.kubernetes.io/master-`{{execute HOST1}}


#### Installing a Pod network add-on 
You must deploy a Container Network Interface (CNI) based Pod network add-on so that your Pods can communicate with each other. 
Cluster DNS (CoreDNS) will not start up before a network is installed.

See a list of add-ons that implement the Kubernetes networking model: https://kubernetes.io/docs/concepts/cluster-administration/networking/#how-to-implement-the-kubernetes-networking-model



We are creating flannel CNI: 
`kubectl apply -f assets/flannel.yml`{{execute HOST1}}

Wait for all the pods to get ready, check the status using the command: 
`watch kubectl get pods --all-namespaces`{{execute HOST1}}

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


Press `cntrl + c` to get exit from the watch command. 

#### Health Check

Again now do the health check to check the status of Master node. 

`kubectl get nodes`{{execute HOST1}}

Output:


| NAME        | STATUS           | ROLES  |  AGE | VERSION|
| ------------- |:-------------:| -----:|-----:|-----:|
| controlplane     | Ready | master| 13m| v1.18.0|


<p style="color:red;"> Now the master node is Ready, which means our Kubernetes cluster is running.  </p>


