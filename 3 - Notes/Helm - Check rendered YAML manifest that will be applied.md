Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
To check rendered YAML manifest that will be applied when installing a Helm chart, we can use the command:
```bash
helm get manifest spark-operator -n <namespace>
```