We need to run `kubeadm` which has been set and configured. 

`kubeadm init --kubernetes-version $(kubeadm version -o short) --pod-network-cidr=10.244.0.0/16`{{execute HOST1}}

#### Health Check

Once started, you can get the status of the cluster with `kubectl cluster-info`{{execute}}

To be sure you have at least one worker node. If you see only master node in the katacode then restart it. (refresh page)
`kubectl get nodes`{{execute}}

Output:


| NAME        | STATUS           | ROLES  |  AGE | VERSION|
| ------------- |:-------------:| -----:|-----:|-----:|
| control-place     | Ready | master| 13m| v1.18.0|