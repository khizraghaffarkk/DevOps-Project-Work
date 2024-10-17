Prometheus, Node Exporter, Mosquitto Exporter, and Grafana Setup
This project involves setting up a monitoring and observability stack for monitoring system metrics using Prometheus, Grafana, Mosquitto exporter, and Node exporter.

## Project Overview
This repository contains Kubernetes deployment and service configurations to set up a monitoring stack. The main components involved are:

- **Prometheus:** Used to scrape and store time-series data.
- **Grafana:** Visualizes the data stored in Prometheus.
- **Mosquitto Exporter:** Exports metrics from Mosquitto broker.
- **Node Exporter:** Exports hardware and OS metrics for monitoring system resources.

## Files in the Repository
**exporter.yaml**
This file configures the Mosquitto exporter as a Kubernetes deployment and service:

- Deployment: Runs a container of sapcc/mosquitto-exporter to collect metrics from the Mosquitto broker.
  
- Service: Exposes the exporter on port 9234 for Prometheus to scrape.
  
**node-exporter.yaml**
This file defines the Node exporter setup:

- Deployment: Deploys the prom/node-exporter container to collect OS and hardware metrics.
  
- Service: Exposes Node exporter on port 9100.
  
**prometheus-grafana.yaml**
This file contains the configurations for deploying Prometheus and Grafana. It includes:

- Prometheus: Configured to scrape metrics from Node exporter, Mosquitto exporter, and other applications running in the namespace.
  
- Grafana: Provides a web interface for visualizing Prometheus metrics, including dashboard setup for system and broker metrics.


## How to Deploy
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

4. Access Grafana: Once deployed, you can access Grafana using the provided credentials in the prometheus-grafana.yaml file.

5. Add Targets to Prometheus: Add the necessary annotations to your applications’ pods for Prometheus to scrape metrics from them.

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
```
## Links for Grafana & Prometheus
- Grafana: [Grafana Dashboard](https://grafana-route-t3testing.rahtiapp.fi/)
- Mosquitto Broker Dashboard: [Mosquitto Broker Dashboard](https://grafana-route-t3testing.rahtiapp.fi/d/wTMoiOPZka/mosquittobroker?orgId=1&refresh=5s)
- Node-Exporter Full Dashboard: [Node-Exporter Full Dashboard](https://grafana-route-t3testing.rahtiapp.fi/d/rYdddlPWk/node-exporter-full?orgId=1)
- Prometheus: [Prometheus Metrics](https://prometheus-route-t3testing.rahtiapp.fi/)


