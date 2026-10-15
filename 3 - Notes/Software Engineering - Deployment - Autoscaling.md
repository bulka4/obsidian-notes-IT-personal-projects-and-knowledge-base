Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Introduction
Autoscaling is a technique of automatically adjusting the amount of computing resources allocated to a workload according to its current or expected demand.

Common signals used to determine whether we need to increase or decrease the amount of resources:
- CPU utilization
- memory utilization
- request rate
- request latency
- queue length
- Kafka consumer lag
- custom application metrics

There are two main forms:
- Horizontal scaling - Change the number of instances (add more servers)
- Vertical scaling - Change the resources of an instance (use a more powerful server, e.g. add CPU or RAM)