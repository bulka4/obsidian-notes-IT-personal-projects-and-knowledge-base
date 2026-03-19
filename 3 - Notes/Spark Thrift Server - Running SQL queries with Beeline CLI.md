Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
We can use Beeline `/opt/spark/bin/beeline` to connect to the Thrift Server and run SQL queries from a command line.

We connect to the Thrift Server using:
```bash
/opt/spark/bin/beeline -u jdbc:hive2://localhost:10000
```
or use dns name or IP address of the server running the Thrift Server instead of `localhost`.