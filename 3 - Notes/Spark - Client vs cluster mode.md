Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Client mode
In the client mode, Spark driver runs where we submit the job. It executes the Spark script we submit and exits.
# Cluster mode
In the cluster mode, new Kubernetes pod is created where Spark driver runs. It runs there all the time and can be used to submit many Spark jobs.