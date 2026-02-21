Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
The metastore is started using the `org.apache.hadoop.hive.metastore.HiveMetaStore` class.

It can be run for example using:
```bash
exec /opt/hadoop/bin/hadoop jar /opt/hive/lib/hive-standalone-metastore-server-4.2.0.jar org.apache.hadoop.hive.metastore.HiveMetaStore
```

where:
- `/opt/hadoop/bin/hadoop jar` means to run a Java program using Hadoop's launcher and classpath ([[Java - Classpath|link]]) (it will include all the Hadoop JARs)
- It includes additionally the `/opt/hive/lib/hive-standalone-metastore-server-4.2.0.jar` JAR
# Checking the start command
If we have a script for starting metastore (like `start-metastore`), we can check what command it uses for starting metastore by running this script in a debug mode ([[Bash - Debug mode|link]]):
```
bash -x start-metastore
```
