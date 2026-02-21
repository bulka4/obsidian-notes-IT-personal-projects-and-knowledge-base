Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
For production deployment with HA (high availability) it is recommended to:
- Use the apache/hive:3.1.3 image 
- Run HiveServer2 and Metastore separately (multiple replicas)
- Use managed PostgreSQL as metadata db with HA (or use replication or clustering on our own)

We can use the SERVICE_NAME env var to select which service to run when running the apache/hive:3.1.3 image:
- metastore - Run only Metastore
- hiveserver2 - Run only HiveServer2
