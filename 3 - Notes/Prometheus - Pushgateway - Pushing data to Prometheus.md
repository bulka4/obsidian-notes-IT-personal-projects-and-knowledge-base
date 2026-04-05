Tags: [[_Monitoring_applications_and_infrastructure]] [[_Prometheus]] [[__Infrastructure_Engineering]]
#MonitoringAppsInfra #Prometheus #InfrastructureEngineering 

# Introduction
A Pushgateway is a tool used to send data to Prometheus whenever we want rather than wait for Prometheus to pull this data.

This is useful when we run job / batch scripts - they run for a specific amount of time and then finishes. They are not supposed to run all the time, e.g. a script performing calculations in a database.

It works like that:
- We send metrics through HTTP to Pushgateway
- Pushgateway stores them in memory
- Prometheus scrapes them from Pushgateway