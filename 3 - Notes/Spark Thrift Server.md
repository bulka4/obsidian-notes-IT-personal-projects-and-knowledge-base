Tags: [[__Data_Engineering]], [[__Distributed_computing]], [[_Spark]]
#DataEngineering #DistributedComputing #Spark

# Introduction
Spark Thrift Server is used to create a long-running Spark session which can be then used in jupyter notebooks or by other applications by connecting through JDBC/ODBC (for example by dbt ([[dbt with Spark|link]])).

It is a Spark driver running in server mode.
# Running on Kubernetes
When running a Spark Thrift Server on Kubernetes, a Spark driver creates dynamically pods running Spark workers and it is exposed via a Kubernetes service.