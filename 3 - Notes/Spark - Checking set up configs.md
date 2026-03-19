Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
In order to confirm whether Spark configs were applied and what values were assigned, we can use this SQL query:
```sql
SET name.of.spark.config;
```
or Python code:
```python
spark.conf.get("spark.sql.catalog.iceberg_catalog", "NOT SET")
```
to get value of the config or return "NOT SET" if it is not set.