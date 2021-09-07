#### Dashboard deployment task

Deploy the dashboard yaml with the command `kubectl apply -f assets/dashboard.yaml`{{execute HOST1}}

The dashboard is deployed into the kubernetes-dashboard namespace. 
View the status of the deployment with `kubectl get pods -n kubernetes-dashboard`{{execute HOST1}}

When the dashboard was deployed, it was assigned a NodePort of 30007. This makes the dashboard available to outside of the cluster and viewable at https://[[HOST_SUBDOMAIN]]-30007-[[KATACODA_HOST]].environments.katacoda.com/
