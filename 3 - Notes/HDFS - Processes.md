Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
In HDFS there is a few main processes (daemons, Java processes):
- NameNode
- DataNode
- Secondary NameNode
### NameNode
**Role**: Manages the file system namespace and metadata. It coordinates work between a client and DataNodes when reading / writing data.

**Responsibilities**:
-  NameNode stores and provides information about:
	-  directory structure, file names, permissions (metadata)
	-  which DataNode has which data blocks
-  Decides in which DataNodes to save data.

**Critical process**: If the NameNode is down, HDFS becomes inaccessible
### DataNode
**Role**: Stores actual data blocks on local disk.

**Responsibilities**:
- Sends heartbeats to NameNode to signal it's alive.
- Reads, writes, stores and replicates data as directed by the client and the NameNode
### Secondary NameNode
**Role**: Helps the primary NameNode handling edit logs. It does that by periodically merging edit logs with the file system image (fsimage).

**Important**:
- It does not replace the NameNode.
- Used to reduce load and prevent edit logs from growing too large

#DataEngineering #DistributedComputing 