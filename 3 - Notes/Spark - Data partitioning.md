Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
When we make calculations on data in Spark, that data is divided into smaller chunks called partitions.

Each partition contains a subset of table records.

On each partition calculations are done separately and in parallel.

For example we might have a table with columns clientName and amount which will be broken into two partitions like that:
![[2 - Images/Spark/Screenshot 1.png]]

#DataEngineering #DistributedComputing 