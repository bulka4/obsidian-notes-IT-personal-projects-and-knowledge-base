Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
Data engineers optimize files.

Questions include:
- partitioning strategy
- file size
- compression
- row groups
- column pruning
- predicate pushdown

Example

Poor partition
```
/year=2026/
```

Good partition
```
year=2026/month=04/day=15/
```

Or perhaps partition by customer or region depending on query patterns.
# File formats
Popular file formats for data storage:
- Parquet
- ORC
- Avro
- Delta Lake
- Apache Iceberg
- Apache Hudi