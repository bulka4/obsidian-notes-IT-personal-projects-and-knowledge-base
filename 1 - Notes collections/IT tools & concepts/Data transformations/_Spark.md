Tags: [[_Spark]] [[__Data_Engineering]], [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

This is a collection of documents related to Spark.

# Materials to learn from
1. [[Spark - Materials to learn from]]
# How Spark works
## Components, processes and communication
1. Submitting jobs (starting calculations):
	1. [[Spark - Clients starting calculations]]
	2. [[Spark - Spark submit CLI tool]]
	3. [[Spark - PySpark CLI tool]]
	4. [[Spark - Running a script with Python]]
2. Modes and resource managers
	1. [[Spark - Components - Master, driver and executors]]
	2. [[Spark - Resource managers]]
	3. [[Spark - Modes]]
3. [[SparkContext]]
4. [[SparkSession]]
5. [[Spark - Configs]]
6. Running Spark in different modes - practical examples:
	1. [[Spark - Setting up a mode when using different clients]]
		1. [[Spark - Setting up a mode with Spark submit]]
		2. [[Spark - Setting up a mode when running a script with Python]]
	2. [[Spark - Configs for running Spark in different modes]]
		1. [[Spark - Running Spark in the client mode - Configs]]
## Calculations in Spark
1. [[Spark - DAG]]
2. [[Spark - Jobs, Stages and Tasks]]
3. [[Spark - Data partitioning]]
4. [[Spark - Input and output partitions, and final output]]
5. [[Spark - Narrow and wide transformation, shuffling]]
6. [[Spark - Calculations performance]]
7. [[Spark - Saving data]]
## Spark SQL
1. [[Spark - Catalog]]
2. [[Spark - Tables metadata]]
3. [[Spark - Managed and external tables]]
# Spark configuration and setup
1. [[Spark - Adding jars]]
## Debugging
1. [[Spark - Specifying configs - debugging]]
2. [[Spark - Checking set up configs]]
# Spark resource managers 
## YARN
1. [[Running Spark on YARN - Lifecycle of a Spark Job on Yarn]]
## Kubernetes
1. [[Spark - Kubernetes as a resource manager]]
2. Submitting jobs
	1. [[Running Spark on Kubernetes - Spark-submit command]]
	2. [[Running Spark on Kubernetes - Spark Operator and SparkApplication CRD]]
3. [[Running Spark on Kubernetes - Spark Operator]]
4. [[Running Spark on Kubernetes - SparkApplication]]
5. [[Spark - Client vs cluster mode]]
## Spark Standalone
1. [[Spark - Standalone resource manager]]
# Thrift Server
1. [[Spark Thrift Server]]
2. [[Spark Thrift Server - External Hive Metastore benefits]]
3. [[Spark Thrift Server - How clients connect]]
4. [[Spark Thrift Server - Starting the Thrift Server]]
5. [[Spark Thrift Server - Running SQL queries with Beeline CLI]]
## Kubernetes deployment
1. [[Spark Thrift Server with an external Hive Metastore - Kubernetes deployment]]
2. [[Spark Thrift Server - Starting the Thrift Server in Kubernetes pod]]
3. [[Spark Thrift Server - Kubernetes deployment - Testing]]
# Spark Operator
1. [[Spark Operator - Introduction]]
## SparkApplication CRD - Implementation details
1. [[SparkApplication CRD - Mounting a volume to an init container]]
2. [[SparkApplication CRD - Dynamic configs (using values from secrets)]]
3. [[SparkApplication CRD - mainApplicationFile - Script to run]]
# Others
1. [[Spark - Monitoring]]
2. [[Spark - Code development]]
# Hive Metastore
# Spark with Iceberg
1. [[Spark with Iceberg]]
2. [[Spark with Iceberg - No Iceberg catalog in the list of catalogs]]
## Iceberg configuration
1. [[Spark - Iceberg configuration]]
# Debugging
1. [[Spark running on Kubernetes - debugging]]