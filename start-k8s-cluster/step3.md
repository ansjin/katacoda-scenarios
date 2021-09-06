## Keadm Installation

#### Keadm Installation on Cloud Side
1. Get Keadm binaries

`wget https://github.com/kubeedge/kubeedge/releases/download/v1.7.2/keadm-v1.7.2-linux-amd64.tar.gz --no-check-certificate`{{execute HOST1}}

2. Unarchive keadm binaries

`tar -xvf keadm-v1.7.2-linux-amd64.tar.gz`{{execute HOST1}}

3. copy them to bin folder

`cp keadm-v1.7.2-linux-amd64/keadm/keadm /usr/local/bin/keadm`{{execute HOST1}}


4. Run keadm

`keadm init --advertise-address=[[KATACODA_HOST1]]`{{execute HOST1}}

5. Create Cloud core service

`ln -s /etc/kubeedge/cloudcore.service /etc/systemd/system/cloudcore.service`{{execute HOST1}}

6. Restart Cloud core service

`sudo service cloudcore start`{{execute HOST1}}

7. Get token and copy it to be used for edge node

`keadm gettoken`{{execute HOST1}}


#### Keadm Installation on Edge Side
1. Get Keadm binaries

`wget https://github.com/kubeedge/kubeedge/releases/download/v1.7.2/keadm-v1.7.2-linux-amd64.tar.gz --no-check-certificate`{{execute HOST2}}

2. Unarchive keadm binaries

`tar -xvf keadm-v1.7.2-linux-amd64.tar.gz`{{execute HOST2}}

3. copy them to bin folder

`cp keadm-v1.7.2-linux-amd64/keadm/keadm /usr/local/bin/keadm`{{execute HOST2}}

4. Join edge node to cloud node

`keadm join --cloudcore-ipport=[[KATACODA_HOST1]]:10000 --token=paste-token-from-above-here`{{execute HOST2}} 