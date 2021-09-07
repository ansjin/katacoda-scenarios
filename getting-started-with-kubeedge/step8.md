By default kubectl cannot access edge node logs, therefore we need to enable them first. 

### Get certificates
Generate the certificates for CloudStream on cloud node, however, 
the generation file is not in the /etc/kubeedge/, we need to copy it from the 
repository.

`wget wget https://raw.githubusercontent.com/kubeedge/kubeedge/master/build/tools/certgen.sh --no-check-certificate`{{execute HOST1}}

`mv certgen.sh /etc/kubeedge/certgen.sh`{{execute HOST1}}

`chmod +x /etc/kubeedge/certgen.sh`{{execute HOST1}}


### Set cloud core ip environment variable
Set `CLOUDCOREIPS` env. The environment variable is set to specify the IP address of cloudcore. 

`export CLOUDCOREIPS=[[HOST1_IP]]`{{execute HOST1}}


### Generate certificates

`./etc/kubeedge/certgen.sh stream`{{execute HOST1}}


### Set ip tables
It is needed to set iptables on the host. (This command should be executed on every apiserver deployed node.)
(In this case, this the master node, and execute this command by root.) 
Run the following command on the host

`iptables -t nat -A OUTPUT -p tcp --dport 10350 -j DNAT --to [[HOST1_IP]]:10003`{{execute HOST1}}

### Change cloudcore.yaml
Modify  `/etc/kubeedge/config/cloudcore.yaml`  to allow: 
`{'cloudStream': {'enable': true}}}`, `{'dynamicController': {'enable': true}}`

`vi /etc/kubeedge/config/cloudcore.yaml`{{execute HOST1}}


### Restart Cloud core service

`pkill cloudcore`{{execute HOST1}}
`nohup cloudcore > cloudcore.log 2>&1 &`{{execute HOST1}}

### Check Cloud core service logs

`cat cloudcore.log`{{execute HOST1}}


### Keadm logs enabling on Edge Side
##### Step1: Modify `{'edgeStream': {'enable': true}}}`, `{'edged': {'clusterDNS': '10.96.0.10'}}`,  `{'edged': {'clusterDomain': 'cluster.local'}}`, `{'metaManager': {'metaServer': {'enable': true}}}`

`vi /etc/kubeedge/config/edgecore.yaml`{{execute HOST2}}


##### Step2: section=Service `Environment="CHECK_EDGECORE_ENVIRONMENT=false"`

`vi /etc/kubeedge/edgecore.service`{{execute HOST2}}


##### Step3: restart Edge core service

`systemctl restart edgecore.service`{{execute HOST2}}


### Restart pods on cloud side which are pending
`kubectl -n kube-system delete pods --field-selector=status.phase=Pending`{{execute HOST1}}