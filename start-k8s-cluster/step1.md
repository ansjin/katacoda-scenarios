We need to run `kubeadm` which has been set and configured. 

`apt-get remove kubelet kubectl kubernetes-cni -y`{{execute HOST2}}

`systemctl daemon-reload`{{execute HOST1}}

`service docker restart`{{execute HOST1}}

`systemctl daemon-reload`{{execute HOST2}}

`service docker restart`{{execute HOST2}}

`docker info | grep -i cgroup`{{execute HOST1}}

`docker info | grep -i cgroup`{{execute HOST2}}

`kubeadm init --kubernetes-version $(kubeadm version -o short) --pod-network-cidr=10.244.0.0/16`{{execute HOST1}}

