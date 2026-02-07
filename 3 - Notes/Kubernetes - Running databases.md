Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Using Kubernetes for databases is not a good idea. Kubernetes is designed for stateless workloads while databases are stateful (they have a state which is their data and it changes over time).

Databases are also latency-sensitive and and consistency-critical, they need to available all the time.

Problems with running databases on Kubernetes:
- Pod restart - When node dies and database pod need to be rescheduled, we need to reattach PVC what takes a lot of time and other applications using that database can crash.
- PVCs + cloud disks can be slow or detach briefly

Kubernetes usually is not needed for running databases because features it provides are not needed. We don't need to (or at least not frequently) restart our database or autoscale it (create replicas of a database).

Running a database outside of Kubernetes might be more reliable and have better performance, plus we don't need to worry about additional configuration when deploying on Kubernetes.