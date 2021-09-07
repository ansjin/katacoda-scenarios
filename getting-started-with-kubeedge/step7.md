### Keadm download

Step1: Get Keadm binaries: `wget https://github.com/kubeedge/kubeedge/releases/download/v1.7.2/keadm-v1.7.2-linux-amd64.tar.gz --no-check-certificate`{{execute HOST2}}

Step2: Unarchive keadm binaries: `tar -xvf keadm-v1.7.2-linux-amd64.tar.gz`{{execute HOST2}}

Step3: copy them to bin folder: `cp keadm-v1.7.2-linux-amd64/keadm/keadm /usr/local/bin/keadm`{{execute HOST2}}



### Join edge node to cloud node
keadm join will install edgecore and mqtt. 
It also provides a flag by which a specific version can be set. Copy the token from cloud side and paste here


`keadm join --cloudcore-ipport=[[HOST1_IP]]:10000 --token=paste-token-from-above-here`{{copy HOST2}} 



### Health Check
Check the nodes in the cloud to see if edge is joined.

`kubectl get nodes`{{execute HOST1}}

Output:


| NAME        | STATUS           | ROLES  |  AGE | VERSION|
| ------------- |:-------------:| ---------:|-----:|---------------:|
| controlplane     | Ready | master| 13m | v1.18.0|
| node01         | Ready    |  agent,edge |   61s |     v1.19.3-kubeedge-v1.7.2 |
