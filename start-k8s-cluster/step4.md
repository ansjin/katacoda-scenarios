## Keadm logs enabling

### Keadm logs enabling on Cloud Side
##### Step1: Get certficates
`wget wget https://raw.githubusercontent.com/kubeedge/kubeedge/master/build/tools/certgen.sh --no-check-certificate`{{execute HOST1}}
`mv certgen.sh /etc/kubeedge/certgen.sh`{{execute HOST1}}
`chmod +x /etc/kubeedge/certgen.sh`{{execute HOST1}}


##### Step2: set cloud core ip

`export CLOUDCOREIPS=[[HOST1_IP]]`{{execute HOST1}}

##### Step3: Get kubeedge tunnelport config map

`kubectl get cm tunnelport -nkubeedge -oyaml`{{execute HOST1}}

##### Step4: set ip tables

`iptables -t nat -A OUTPUT -p tcp --dport 10350 -j DNAT --to [[HOST1_IP]]:10003`{{execute HOST1}}

##### Step5: change cloud `{'cloudStream': {'enable': true}}}`, `{'dynamicController': {'enable': true}}`

`vi /etc/kubeedge/config/cloudcore.yaml`{{execute HOST1}}

##### Step6: restart Cloud core service

`systemctl restart cloudcore.service`{{execute HOST1}}



### Keadm logs enabling on Edge Side
##### Step1: Modify `{'edgeStream': {'enable': true}}}`, `{'edged': {'clusterDNS': '10.96.0.10'}}`,  `{'edged': {'clusterDomain': 'cluster.local'}}`, `{'metaManager': {'metaServer': {'enable': true}}}`

`vi /etc/kubeedge/config/edgecore.yaml`{{execute HOST2}}


##### Step2: section=Service `Environment="CHECK_EDGECORE_ENVIRONMENT=false"`

`vi /etc/kubeedge/edgecore.service`{{execute HOST2}}


##### Step3: restart Edge core service

`systemctl restart edgecore.service`{{execute HOST2}}


### Restart pods on cloud side which are pending
`kubectl -n kube-system delete pods --field-selector=status.phase=Pending`{{execute HOST1}}