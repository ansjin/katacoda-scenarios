### Prepare the environmennt for both nodes.
We need to have cgroupfs as the cgroup runtime therefore run these:

Remove kubernetes related packages from the edge node: 
`apt-get remove kubelet kubectl kubernetes-cni -y`{{execute HOST2}}

Download docker `daemon.json` file with cgroupfs as cgroup runntime: 
`wget https://raw.githubusercontent.com/ansjin/katacoda-scenarios/main/getting-started-with-kubeedge/assets/daemon.json`{{execute HOST2}}

Move `daemon.json` to `/etc/docker/daemon.json`: 
`mv daemon.json /etc/docker/daemon.json`{{execute HOST2}}

Reload docker on Host1: 
`systemctl daemon-reload`{{execute HOST1}}

`service docker restart`{{execute HOST1}}

Reload docker on Host2:
`systemctl daemon-reload`{{execute HOST2}}

`service docker restart`{{execute HOST2}}

Check cgroup runtime on Host1: 
`docker info | grep -i cgroup`{{execute HOST1}}

Output will be something like this: 

<pre>
controlplane $ docker info | grep -i cgroup
WARNING: No swap limit support
WARNING: the overlay storage-driver is deprecated, and will be removed in a future release.
 Cgroup Driver: cgroupfs
 
</pre> 
 
Check cgroup runtime on Host2: 
`docker info | grep -i cgroup`{{execute HOST2}}

Output will be something like this: 

<pre>
node01 $ docker info | grep -i cgroup
WARNING: No swap limit support
WARNING: the overlay storage-driver is deprecated, and will be removed in a future release.
 Cgroup Driver: cgroupfs
 
</pre> 