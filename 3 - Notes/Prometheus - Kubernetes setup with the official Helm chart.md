Tags: [[_Monitoring_applications_and_infrastructure]] [[_Prometheus]] [[__Infrastructure_Engineering]]
#MonitoringAppsInfra #Prometheus #InfrastructureEngineering 

# Introduction
Using the `prometheus-community/kube-prometheus-stack` official Helm chart we can install:
- Prometheus
- Grafana

and two exporters ([[Prometheus - Exporters|link]]) which provide data about Kubernetes to Prometheus:
- node-exporter
- kube-state-metrics
# Installation
We install it using:
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm install monitoring prometheus-community/kube-prometheus-stack
```
# node-exporter
Runs on every node and gives:
- CPU usage
- memory usage
- disk I/O
# kube-state-metrics
Runs as a single pod and gives:
- pod states
- deployments
- replicas
- restarts
