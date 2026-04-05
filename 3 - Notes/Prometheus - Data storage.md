Tags: [[_Monitoring_applications_and_infrastructure]] [[_Prometheus]] [[__Infrastructure_Engineering]]
#MonitoringAppsInfra #Prometheus #InfrastructureEngineering 

# Introduction
Prometheus stores data locally in its own database. It is a time-series database and data looks like this:
```
metric_name{label1="value1"} = value over time
```

It is stored on disk in:
```
/var/lib/prometheus/
```

There is a retention policy. Data is being deleted after specified period of time.
# Separate database
Database can be managed and tied to Prometheus, i.e. when we restart Prometheus, we restart also the database and they can't be scaled separately (they are one process).

Database can be also deployed separately. Popular choices for database for Prometheus includes Thanos, Cortex or VictoriaMetrics. 