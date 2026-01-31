Tags: [[__Data_storage]]
#DataStorage

# Introduction
A catalog is a system that stores and provides metadata about data objects - what exists, where it is and how to read it.

Examples of catalogs include:
- System catalog / information schema (used by SQL databases)
- Hive Metastore (used by Spark)
# Information catalog provides
For example, a catalog provides metadata about:
- Databases / schemas
- Tables / views
- Columns (names and data types)
- Statistics (row counts, sizes)
- Ownership / permissions
# Spark example
When we want to read data using Spark without a catalog, we need to provide a full path to the file which stores data:
```sql
SELECT * FROM parquet.`abfss://data@lake/raw/events`;
```
If we are using a catalog, for example a Hive Metastore, we can use a table name:
```sql
SELECT * FROM raw.events
```
and Spark will find in the catalog where data for the `raw.events` is stored.