### Keadm download

Step1: Get Keadm binaries: `wget https://github.com/kubeedge/kubeedge/releases/download/v1.7.2/keadm-v1.7.2-linux-amd64.tar.gz --no-check-certificate`{{execute HOST1}}

Step2: Unarchive keadm binaries: `tar -xvf keadm-v1.7.2-linux-amd64.tar.gz`{{execute HOST1}}

Step3: copy them to bin folder: `cp keadm-v1.7.2-linux-amd64/keadm/keadm /usr/local/bin/keadm`{{execute HOST1}}



### Run keadm init
By default ports `10000` and `10002` in cloudcore needs to be accessible for the edge nodes.

keadm init will install cloudcore, generate the certs and install the CRDs. 
It also provides a flag by which a specific version can be set.

`keadm init --advertise-address=[[HOST1_IP]]`{{execute HOST1}}

### Check logs of Cloud core service to see everything is running

`cat /var/log/kubeedge/cloudcore.log`{{execute HOST1}}

### Create Cloud core service

`ln -s /etc/kubeedge/cloudcore.service /etc/systemd/system/cloudcore.service`{{execute HOST1}}

### Restart Cloud core service

`sudo service cloudcore restart`{{execute HOST1}}


### Get token and copy it to be used for edge node
This will be used when joining edge nodes.

`keadm gettoken`{{execute HOST1}}


### Keadm Installation on Edge Side
##### Step1: Get Keadm binaries

`wget https://github.com/kubeedge/kubeedge/releases/download/v1.7.2/keadm-v1.7.2-linux-amd64.tar.gz --no-check-certificate`{{execute HOST2}}

##### Step2: Unarchive keadm binaries

`tar -xvf keadm-v1.7.2-linux-amd64.tar.gz`{{execute HOST2}}

##### Step3: copy them to bin folder

`cp keadm-v1.7.2-linux-amd64/keadm/keadm /usr/local/bin/keadm`{{execute HOST2}}

##### Step4: Join edge node to cloud node

`keadm join --cloudcore-ipport=[[HOST1_IP]]:10000 --token=paste-token-from-above-here`{{copy HOST2}} 


### Health Check

`kubectl get nodes`{{execute HOST1}}

Output:


| NAME        | STATUS           | ROLES  |  AGE | VERSION|
| ------------- |:-------------:| ---------:|-----:|---------------:|
| controlplane     | Ready | master| 13m | v1.18.0|
| node01         | Ready    |  agent,edge |   61s |     v1.19.3-kubeedge-v1.7.2 |
