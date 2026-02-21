Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
This document describes how to use Docker images to deploy Hive Metastore and HiveServer2 with PostgreSQL as metadata db.
# apache/hive:3.1.3 image
When using the apache/hive:3.1.3 image, we can use the SERVICE_NAME env var to select which service to run:
- metastore
- hiveserver2

so we don't need to run both those services together. Running only one service helps for example to save memory (running both requires a lot of memory, probably above 6GB).
# apache/hive:standalone-metastore-4.2.0
This image is smaller than apache/hive:3.1.3 but there is a problem with adding the PostgreSQL driver jar library so we can use PostgreSQL as metadata db. 

We are getting error when running `hive/bin/start-metastore` script:
```
There is no available StoreManager of type "jdbc". Make sure that you have put the relevant DataNucleus store plugin in your CLASSPATH
```
and we don't know for now how to add this driver to the classpath ([[Hive setup - Adding jars to the classpath|link]]) which is used.

Initialization of schema using `schematool -dbType postgres -initSchema` works.
## Solutions tried and errors
- Run `bash -x /opt/hive/bin/start-metastore` to see what commands it executes
- This command is used to start hive metastore in the `start-metastore` script:
```bash
exec /opt/hadoop/bin/hadoop jar /opt/hive/lib/hive-standalone-metastore-server-4.2.0.jar org.apache.hadoop.hive.metastore.HiveMetaStore
```
- When I run:
	```bash
	exec java -cp "/opt/hive/lib/*" \ 
		org.apache.hadoop.hive.metastore.HiveMetaStore
	```
	It says:
	```bash
	Error: Unable to initialize main class org.apache.hadoop.hive.metastore.HiveMetaStore Caused by: java.lang.NoClassDefFoundError: org/apache/hadoop/conf/Configurable
	```
- Using `export HADOOP_CLASSPATH=/opt/hive/lib/*` doesn't help
- `/opt/hive/lib` contains:
	- `datanucleus-core-6.0.10.jar`
	- `datanucleus-api-jdo-6.0.3.jar`
	- `datanucleus-rdbms-6.0.10.jar`
	- PostgreSQL driver jar
- `/opt/hadoop/bin/hadoop classpath` shows the hive/lib folder content
- Copy `hive/lib/postgresql-42.x.jar` into `/opt/hadoop/share/hadoop/common/lib/`
- I tried running:
```bash
java -cp "/opt/hive/lib/*:/opt/hadoop/share/hadoop/common/*:/opt/hadoop/share/hadoop/common/lib/*:/opt/hadoop/share/hadoop/hdfs/*:/opt/hadoop/share/hadoop/hdfs/lib/*:/opt/hadoop/share/hadoop/mapreduce/*:/opt/hadoop/share/hadoop/yarn/*" \ org.apache.hadoop.hive.metastore.HiveMetaStore
```