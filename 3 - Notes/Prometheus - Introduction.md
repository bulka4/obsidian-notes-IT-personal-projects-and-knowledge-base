Tags: [[_Monitoring_applications_and_infrastructure]] [[_Prometheus]] [[__Infrastructure_Engineering]]
#MonitoringAppsInfra #Prometheus #InfrastructureEngineering 

# Introduction
Prometheus is used to collect and store metrics from systems which can be used for monitoring those systems.

It runs as a single process which is responsible for:
- Scraping ([[Prometheus - Scraping|link]])
- Storage
- Querying
- Alerting

Prometheus does NOT wait for data. It pulls (scrapes) data from targets by making Rest API calls. So targets from which we want to take metrics, need to expose a Rest API endpoint.
# Questions
- 