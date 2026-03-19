Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
Before we start metastore, we need to initialize schema - [[Hive setup - Initializing schema]].

Then we can start metastore in different ways:
- Run the `HiveMetaStore` class using Hadoop
- Run the `hive --service metastore` command
- Use the start script `start-metastre` (available only in some of the Hive distributions)
- Using Java directly
# Run the `HiveMetaStore` class using Hadoop
The metastore is started using the `org.apache.hadoop.hive.metastore.HiveMetaStore` class.

It can be run for example using:
```bash
exec /opt/hadoop/bin/hadoop jar /opt/hive/lib/hive-standalone-metastore-server-4.2.0.jar org.apache.hadoop.hive.metastore.HiveMetaStore
```

where:
- `/opt/hadoop/bin/hadoop jar` means to run a Java program using Hadoop's launcher and classpath ([[Java - Classpath|link]]) (it will include all the Hadoop JARs)
- It includes additionally the `/opt/hive/lib/hive-standalone-metastore-server-4.2.0.jar` JAR
# Java directly
We can start Hive metastore using Java directly:
```bash
java -cp "$HIVE_HOME/lib/*:$HADOOP_HOME/share/hadoop/common/*:..." \
  org.apache.hadoop.hive.metastore.HiveMetaStore
```
where `-cp` defines the classpath to use ([[Java - Classpath|link]]).
# Start script (check what commands it executes)
If we have a script for starting metastore (like `start-metastore`), we can check what command it uses for starting metastore by running this script in a debug mode ([[Bash - Debug mode|link]]):
```
bash -x start-metastore
```
