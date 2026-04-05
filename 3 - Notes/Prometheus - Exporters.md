Tags: [[_Monitoring_applications_and_infrastructure]] [[_Prometheus]] [[__Infrastructure_Engineering]]
#MonitoringAppsInfra #Prometheus #InfrastructureEngineering 

# Introduction
When a system doesn't support Prometheus (doesn't make metrics available for it), we can use an exporter which queries the system (takes data from it) and makes it available to Prometheus as a Rest API endpoint.

An exporter is like a translator - it doesn't store data but it only talks to a system, takes data from it and sends to Prometheus, when Prometheus sends a Rest API request to the exporter.

For example, in order to take data from a system, an exporter can:
- Run a SQL query
- Read system files
- Use internal APIs

An exporter is typically a long-running process that exposes an HTTP endpoint (usually `/metrics`) and responds to Prometheus scrape requests.
