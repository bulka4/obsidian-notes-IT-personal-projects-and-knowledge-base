Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
Hive Thrift just like HiveServer2 ([[Hive - HiveServer2|link]]) is used to execute SQL queries:
- It receives a SQL query from a client
- Uses Hive Metastore ([[Hive - Metastore|link]]) to get necessary metadata to compile a SQL query (decide how to execute it)
- Executes SQL queries using chosen engine (MapReduce, Tez, or Spark)
- Returns results to the client

But it has less functionalities:
- No multi-user support (when multiple users want to execute sql queries at the same time)
- Weaker security and authentication
- Limited JDBC / ODBC support for clients to connect to Hive Thrift