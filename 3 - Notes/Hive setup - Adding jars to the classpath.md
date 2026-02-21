Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
Hive is using jars (Java libraries) to work (for example a PostgreSQL driver for connecting to a metadata db). Those jars need to be included in the classpath ([[Java - Classpath|link]]) used by Hive.

Usually the `/opt/hive/lib` folder is automatically included in the classpath when we use Hive's startup scripts.

The `HADOOP_CLASSPATH` environment variable can be used to add additional jars to the classpath used by Hadoop (i.e. used by Hive among the others). Hadoop builds its classpath from:
- Its own internal Hadoop jars
- Config directories (`HADOOP_CONF_DIR` env var)
- Anything listed in `HADOOP_CLASSPATH`