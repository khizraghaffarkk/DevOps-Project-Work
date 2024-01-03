oc new-app --template=openshift/prometheus-grafana -p NAMESPACE=csc_project_name

oc new-project csc_project_name --description="This is Project Work"

oc new-app -f ./prometheus-grafana.yaml -p NAMESPACE=csc_project_name

oc apply -f ./prometheus-grafana.yaml -n csc_project_name


kubectl get configmap prometheus-config -n csc_project_name -o yaml

---------- exporter.yaml------------
oc apply -f exporter.yaml
oc logs mosquitto-exporter-<pod-id>

oc apply -f node-exporter.yaml

oc apply -f prometheus-grafana.yaml

Mosquitto Broker Dashboard: 
https://grafana-route-t3testing.rahtiapp.fi/d/wTMoiOPZka/mosquitto-broker?orgId=1&refresh=5s

Node-Exporter-Dashboard:
https://grafana-route-t3testing.rahtiapp.fi/d/rYdddlPWk/node-exporter-full?orgId=1&var-datasource=prometheus&var-job=node-exporter&var-node=node-exporter-service.t3testing.svc:9100&var-diskdevices=%5Ba-z%5D%2B%7Cnvme%5B0-9%5D%2Bn%5B0-9%5D%2B%7Cmmcblk%5B0-9%5D%2B

Grafana Dashboard:
       
Prometheus Dasboard:

------------
Delete the Routes:

oc delete route grafana-route -n csc_project_name
oc delete route prometheus-route -n csc_project_name

Delete Deployments:

oc delete deployment grafana-1 -n csc_project_name
oc delete deployment mosquitto-exporter -n csc_project_name
oc delete deployment prometheus-1 -n csc_project_name
Delete Services:

Delete Services:

oc delete service grafana-service -n csc_project_name
oc delete service mosquitto-exporter-service -n csc_project_name
oc delete service prometheus-service -n csc_project_name
Delete Persistent Volume Claims (if applicable):

Delete Persistent Volume Claims (if applicable):

oc delete pvc grafana-data -n csc_project_name
oc delete pvc prometheus-data -n csc_project_name
Delete ConfigMaps and Secrets:

Delete ConfigMaps and Secrets:

oc delete configmap grafana-config -n csc_project_name
oc delete configmap prometheus-config -n csc_project_name

oc delete secret grafana-secret -n csc_project_name
Verify that Resources are Deleted:

oc get all -n csc_project_name

oc logs <grafana-pod>