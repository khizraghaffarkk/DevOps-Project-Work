# DevOps Project - Task 2

## Overview

This repository contains the configuration files and templates necessary for setting up a monitoring system using **Prometheus**, **Grafana**, **Mosquitto Exporter**, and **Node Exporter**. The project aims to facilitate the monitoring of applications and services running within a Kubernetes cluster.

## Contents

- `exporter.yaml`: Configuration for deploying Mosquitto Exporter.
- `node-exporter.yaml`: Configuration for deploying Node Exporter.
- `prometheus-grafana.yaml`: Template for deploying Prometheus and Grafana, including the necessary configurations for monitoring metrics.

## Task 2 Description

### Objective

The objective of Task 2 is to set up a monitoring solution that includes the following components:

- **Mosquitto Exporter**: To collect metrics from a Mosquitto MQTT broker.
- **Node Exporter**: To expose hardware and OS metrics from the host machine.
- **Prometheus**: To scrape and store metrics data.
- **Grafana**: To visualize the metrics collected by Prometheus.

### Setup Instructions

1. **Deploy Mosquitto Exporter**:
   Use the `exporter.yaml` file to deploy the Mosquitto Exporter. This will create a deployment and a service to expose metrics.

   ```bash
   kubectl apply -f exporter.yaml
   ```
   
2. Deploy Node Exporter: Use the node-exporter.yaml file to deploy Node Exporter.
   ```bash
   kubectl apply -f node-exporter.yaml
   ```

3. Deploy Prometheus and Grafana: Use the prometheus-grafana.yaml file to set up Prometheus and Grafana.
   ```bash
   oc process -f prometheus-grafana.yaml | oc apply -f -
   ```
- Ensure to replace the environment variables for PROMETHEUS_IMAGE, GRAFANA_IMAGE, BASIC_AUTH_USERNAME, and BASIC_AUTH_PASSWORD as required.

## Accessing Prometheus and Grafana
After deploying the above configurations, you will be able to access Prometheus and Grafana through the OpenShift project overview page.

**1. Grafana Admin Credentials:**

- **Username:** ${GRAFANA_ADMIN_USERNAME}
- **Password:** ${GRAFANA_ADMIN_PASSWORD}

**2. Prometheus Basic Auth Credentials:**

- **Username:** ${BASIC_AUTH_USERNAME}
- **Password:** ${BASIC_AUTH_PASSWORD}

## Monitoring Applications
To monitor your applications with Prometheus, add the following annotations to the pods you want to scrape metrics from:
```yaml
annotations:
  prometheus.io/scrape: 'true'
  prometheus.io/path: <path>  # Optional, defaults to '/metrics'
  prometheus.io/port: <port>    # Optional, defaults to the pod's declared port















====================================
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
