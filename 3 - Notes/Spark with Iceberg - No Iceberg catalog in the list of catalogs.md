Tags: [[_Spark]] [[__Data_Engineering]], [[__Distributed_computing]] [[_Iceberg]]  [[Object storage]] 
#Spark #DataEngineering #DistributedComputing #Iceberg #ObjectStorage 

# Introduction
When using Spark with Iceberg, and we create an Iceberg catalog, this catalog might exist and we might be able to use it properly but when running:
```sql
show catalogs;
```
we might see only the default `spark_catalog`, without the Iceberg catalog.