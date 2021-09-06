We need to run `kubeadm` which has been set and configured. 

`kubeadm init --kubernetes-version $(kubeadm version -o short) --pod-network-cidr=10.244.0.0/16`{{execute HOST1}}

