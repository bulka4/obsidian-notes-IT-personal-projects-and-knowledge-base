Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
We can check available fields with descriptions for a specific resource by using:
```bash
kubectl explain <resource-type>.<field_1>.<field_2>
```
for example `resource-type` can be a `pod`, `field_1` can be `spec` and `field_2` can be `containers`.