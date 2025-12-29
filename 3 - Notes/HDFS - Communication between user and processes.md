Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
### User => client
Users always talk to client first and then client talks to other HDFS processes (NameNode, DataNode etc).
### Reading data
When client wants to read data, then communication looks like that:
- Client sends a request to the NameNode to read data.
- NameNode identifies which DataNodes have the data and sends that info back to the client.
- Client then contacts the proper DataNodes directly to read the data.
### Writing data
When a client wants to write data, then communication looks like this:
- The client sends a request to the NameNode to create a file.
- The NameNode selects appropriate DataNodes to store data (including replicas)
- The client pushes the data directly to the frist DataNode, which forwards it to other DataNodes to create the replicas.

No data is sent thorugh the NameNode. It only handles metadata and coordination.

#DataEngineering #DistributedComputing 