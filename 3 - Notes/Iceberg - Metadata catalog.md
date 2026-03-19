Tags: [[_Iceberg]] [[__Data_Engineering]] [[Object storage]] 
#Iceberg #DataEngineering #ObjectStorage 

# Introduction
In Iceberg, a catalog has two meanings - it is a logical group of schemas and tables as explained here - [[Iceberg - Data structure|link]],  and it is also a metadata db.
# Catalog as a metadata db
Iceberg creates a catalog which is a collection of metadata stored in object storage. That metadata allows for execution of SQL queries, just like Hive.

It can be used together with Hive, such that Hive stores table name, type and location where data is stored, and Iceberg stores snapshots, schema and partitions metadata, and version history which are used for Iceberg features such as time travel or ACID transactions.

Iceberg's metadata is saved together with data in the same folder representing a table.

