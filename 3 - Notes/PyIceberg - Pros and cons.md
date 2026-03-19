Tags: [[_Iceberg]] [[__Data_Engineering]], [[Object storage]] 
#Iceberg #DataEngineering #ObjectStorage 

# Cons
PyIceberg might struggle when writing data. It is not as mature as Spark and some advanced features might be missing or slower:
- complex partition writes
- high-concurrency writers
- advanced compaction workflows

but for 'regular' writing data it is fine.