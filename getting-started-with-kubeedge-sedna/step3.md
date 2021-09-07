The cluster has now been initialised. 
The Master node will manage and run the pods on cloud side in our cluster, since there is no worker node.


#### Copy kube config file
To manage the Kubernetes cluster, the client configuration and certificates are required. 
This configuration is created when _kubeadm_ initialises the cluster. 
The command copies the configuration to the users home directory and sets the environment variable for use with the CLI.

`mkdir -p $HOME/.kube`{{execute HOST1}}

`sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config`{{execute HOST1}}

`sudo chown $(id -u):$(id -g) $HOME/.kube/config`{{execute HOST1}}

#### Health Check
The Kubernetes CLI, known as _kubectl_, can now use the configuration to access the cluster. 
Once started, you can get the status of the cluster with `kubectl cluster-info`{{execute}}

Check the nodes in cluster
`kubectl get nodes`{{execute}}
You will see only master node in the katacode.


Output:


| NAME        | STATUS           | ROLES  |  AGE | VERSION|
| ------------- |:-------------:| -----:|-----:|-----:|
| controlplane     | NotReady | master| 13m| v1.18.0|

<p style="color:red;"> Check the NotReady status of master node </p>



