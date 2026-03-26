Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
In the SparkApplication CRD, the `spec.mainApplicationFile` field, we specify the path to the script to run. It can be:
- A local file in the image - then we use the `local:///path_to_script` path
- File in cloud - then we provide URL to that file