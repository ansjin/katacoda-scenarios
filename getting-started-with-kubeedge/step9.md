### Modify edgecore.yaml
Modify  `/etc/kubeedge/config/edgecore.yaml`  to allow: 

`{'edgeStream': {'enable': true}}}`, 

`{'edged': {'clusterDNS': '10.96.0.10'}}`, 
 
`{'edged': {'clusterDomain': 'cluster.local'}}`, 

`{'metaManager': {'metaServer': {'enable': true}}}`


`vi /etc/kubeedge/config/edgecore.yaml`{{execute HOST2}}


### Avoid Kube-proxy

kubeedge reject kube-proxy  by default, it use a succedaneum called edgemesh.

Ask edgecore not to check the environment by adding the env variable in edgecore.service :

`Environment="CHECK_EDGECORE_ENVIRONMENT=false"`{{copy HOST2}}

`vi /etc/kubeedge/edgecore.service`{{execute HOST2}}

the file should look like this:

```
Description=edgecore.service

[Service]
Type=simple
ExecStart=/root/cmd/ke/edgecore --logtostderr=false --log-file=/root/cmd/ke/edgecore.log
Environment="CHECK_EDGECORE_ENVIRONMENT=false"

[Install]
WantedBy=multi-user.target

```

### Restart Edge core service

`systemctl restart edgecore.service`{{execute HOST2}}


### Restart pods on cloud side which are pending
`kubectl -n kube-system delete pods --field-selector=status.phase=Pending`{{execute HOST1}}

### Check all pods status
Wait for all the pods to get ready, check the status using the command: 
`watch kubectl get pods --all-namespaces`{{execute HOST1}}
