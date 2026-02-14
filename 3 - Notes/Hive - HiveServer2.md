Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
HiveServer2 acts as the gateway between users/tools and Hive:
- Accepts SQL queries from clients (BI tools, notebooks, apps)
- Manages sessions and authentication
- Uses Hive Metastore ([[Hive - Metastore|link]]) to get metadata needed to compile SQL queries (decide how to execute them)
- Executes SQL queries using chosen engine (MapReduce, Tez, or Spark)
- Returns results to clients

HiveServer2 is the service that allows multiple users and applications to safely and efficiently run SQL queries on Hive.
# How clients connect
Clients connect to HiveServer2 using JDBC or ODBC drivers.
# Purpose and benefits
It replaced the older Hive CLI / Hive Thrift Server to solve major limitations:
- Multi-user concurrency
- Better security (Kerberos, LDAP, SSL)
- Session isolation
- High availability support
- Authentication & authorization
- Connection pooling
- Supports load balancers
- Designed for production workloads
# Communication
Communication looks like that:
```yaml
Client (Beeline / BI Tool)
        |
        v
   HiveServer2
        |
        v
   Hive Metastore
        |
        v
Execution Engine (Spark / Tez / MapReduce)
        |
        v
   HDFS / Object Storage
```
# Alternatives
HiveServer2 is not necessary for using Metastore to compile and run SQL queries. Other tools (like Spark) can also use Metastore directly to compile and run SQL queries.