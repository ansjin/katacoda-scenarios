### Start the kubernetes cluster using kubeadm

Kubeadm solves the problem of handling TLS encryption configuration, deploying the core Kubernetes components and ensuring that additional nodes can easily join the cluster. The resulting cluster is secured out of the box via mechanisms such as RBAC.

More details on Kubeadm can be found at https://github.com/kubernetes/kubeadm


We need to run `kubeadm` which has been set and configured. 

`kubeadm init --kubernetes-version $(kubeadm version -o short) --pod-network-cidr=10.244.0.0/16`{{execute HOST1}}

