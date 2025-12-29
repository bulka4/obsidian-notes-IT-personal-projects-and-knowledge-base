Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
Each task performs transformations on a single data partition which is called an **input partition.**

A result of those transformations is also a single data partition and it is called an **output partition.**

How the final output is created:
- A single job can consist of multiple tasks
- Each task takes as input a single data partition and produces a single output partition
- All the output partitions are combined together to create a final job output.

#DataEngineering #DistributedComputing 