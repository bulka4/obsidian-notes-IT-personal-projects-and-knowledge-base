Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
We can have multiple replicas of the same app (Pod). That means that we have multiple copies of the same app running. It is useful because when one app goes down, then the other one can take its place in handling requests.

We can use a Service (described in the previous section) to create a static IP address, and each request made to that IP address will be redirected by a Service to a replica which is the least busy.
