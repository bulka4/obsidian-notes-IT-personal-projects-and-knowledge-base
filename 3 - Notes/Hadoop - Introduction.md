Tags: [[_Hadoop]] 
#Hadoop 

# Introduction
Hadoop has two parts:
- Hadoop cluster services - Like HDFS, YARN, MapReduce
- Hadoop libraries - Java libraries like `hadoop-common`, `hadoop-hdfs`, `hadoop-azure`. They are used by every cluster service and they provide for example: 
	- FileSystem abstraction
	- Configuration system
	- Input/output APIs
	- Pluggable storage drivers (S3, ABFS, HDFS, etc.)