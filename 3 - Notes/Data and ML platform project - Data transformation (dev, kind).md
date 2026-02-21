Tags: [[_My_projects]]
#MyProjects 

# Hive
We use a small image containing only Hive Metastore, without HiveServer2 and other, unnecessary libraries and jars which uses a lot of memory.
## Image to use
We use apache/hive:3.1.3 image. We use it to run only a Metastore without HiveServer2 (which is not needed for now and uses a lot of memory).

We were also trying the apache/hive:standalone-metastore-4.2.0 but there were problems as described here - [[Hive setup - Docker image to use]].
## Hive CLI
- In order to use Hive CLI:
	- From the pod running Hive Metastore:
		- Use the `hive --hiveconf hive.metastore.uris=thrift://localhost:9083` command
	- From other pods:
		- Use the `hive --hiveconf hive.metastore.uris=thrift://{{ .Release.Name }}-hive-metastore:9083` command
## Datawarehouse
For data storage (specified in the `hive-site.xml` as the `hive.metastore.warehouse.dir` config) we use for now local storage. We can change it into Azure Storage Account.
### PV
We need to use the same PV (from the `common` helm chart) for data warehouse mounted into the same path into both pods running the Hive Metastore and Spark Thrift Server.

Path where this PV is mounted needs to be specified in:
- The `spark.sql.warehouse.dir` config in the Spark's pod, in the `hive-site.xml` file
- The `hive.metastore.warehouse.dir` config in the Hive's pod, in the `hive-site.xml` file
# Spark Thrift Server
Clients (dbt) can connect to the Spark Thrift Server ([[Spark Thrift Server - How clients connect|link]]) and send SQL queries to execute using:
- JDBC or ODBC drivers
- Thrift protocol 

Thrift Server will use Hive Metastore to retrieve necessary metadata to execute that SQL query.
# dbt
We use the Thrift protocol to connect to the Spark Thrift Server and send SQL queries to execute.
# Problems
## Spark local data storage
There is a problem when we want to use localhost filesystem as a storage for Spark data, i.e. when the `spark.sql.warehouse.dir` config points to a folder in a local filesystem which is a mounted volume which stores data on the localhost using the `hostPath` parameter.

When trying to create a new database `dwh_fact` and table in it, we get an error:
```
Cannot create staging directory  'file:/shared/warehouse/dwh_fact.db/model/.hive-staging_hive_2026-02-20_09-46-34_493_8165871989128179421-1
```
where `spark.sql.warehouse.dir=/shared/warehouse` is the mounted volume.

Issue might be related to file permissions, even though we tried to set up:
- `spark.sql.warehouse.dir.filePermissionMask=0777` in the Spark config
- `hive.scratchdir.permission=0777` in the Hive config
which causes that every new folder created by Spark and Hive has read/write permissions for everyone (`dwh_fact.db` is such a folder created by Hive).

So Spark should be able to write to `/shared/warehouse/dwh_fact.db` but for some reason we still get this error.
### Solution
Solution might be to use cloud object storage instead of a local filesystem to avoid issues with file permissions.
# To do
## dbt
- Create a testing pod: `kubectl apply -f dbt.yaml`
- Test connectivity to the Thrift Server: `python test_spark_connection.py`
- run dbt project:
```bash
dbt debug
dbt run
```
# Questions
- 