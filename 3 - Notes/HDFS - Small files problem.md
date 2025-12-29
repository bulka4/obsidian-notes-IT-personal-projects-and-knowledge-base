Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
HDFS has problems when we want to store in it a lot of small files. That’s because:
-  Each data block can store only one file
	- For example if our file has 8mb and block size is 128mb, then the entire block will be used only for storing this one file, so the remaining 120mb will be unused.
-  NameNode needs to handle metadata of all the files
	- There is only one NameNode which needs to handle metadata of all the files.
	- If there is too many files, there can be too much metadata for the NameNode to handle.
	- We can use the HDFS Federation to create multiple NameNodes.

#DataEngineering #DistributedComputing 