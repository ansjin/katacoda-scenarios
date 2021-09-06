## Keadm Installation

### Keadm Installation on Cloud Side
##### Get Keadm binaries

`wget https://github.com/kubeedge/kubeedge/releases/download/v1.7.2/keadm-v1.7.2-linux-amd64.tar.gz --no-check-certificate`{{execute HOST1}}

##### Unarchive keadm binaries

`tar -xvf keadm-v1.7.2-linux-amd64.tar.gz`{{execute HOST1}}

##### copy them to bin folder

`cp keadm-v1.7.2-linux-amd64/keadm/keadm /usr/local/bin/keadm`{{execute HOST1}}

##### Get host IP address

`hostip=$(hostname -I | awk '{print $1}')`{{execute HOST1}}


##### Run keadm

`keadm init --advertise-address=$hostip`{{execute HOST1}}

##### Create Cloud core service

`ln -s /etc/kubeedge/cloudcore.service /etc/systemd/system/cloudcore.service`{{execute HOST1}}

##### Restart Cloud core service

`sudo service cloudcore restart`{{execute HOST1}}

##### Check logs of Cloud core service to see everything is running

`cat /var/log/kubeedge/cloudcore.log`{{execute HOST1}}


##### Get token and copy it to be used for edge node

`keadm gettoken`{{execute HOST1}}


### Keadm Installation on Edge Side
##### Get Keadm binaries

`wget https://github.com/kubeedge/kubeedge/releases/download/v1.7.2/keadm-v1.7.2-linux-amd64.tar.gz --no-check-certificate`{{execute HOST2}}

##### Unarchive keadm binaries

`tar -xvf keadm-v1.7.2-linux-amd64.tar.gz`{{execute HOST2}}

##### copy them to bin folder

`cp keadm-v1.7.2-linux-amd64/keadm/keadm /usr/local/bin/keadm`{{execute HOST2}}

##### Join edge node to cloud node

`keadm join --cloudcore-ipport=[[KATACODA_HOST1]]:10000 --token=paste-token-from-above-here`{{copy HOST2}} 