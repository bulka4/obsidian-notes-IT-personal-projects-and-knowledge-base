Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
Hive uses jars (Java libraries) to work. They bring different functionalities to Hive, for example a PostgreSQL driver for connecting to a PostgreSQL metadata db or jars for connecting to cloud object storage. 

Those jars need to be included in the classpath ([[Java - Classpath|link]]) used by Hive so Hive can use them.
# Hive classpath
Hive classpath is created from multiple sources:
- Hadoop classpath
- `$HIVE_HOME/lib` folder
- `HIVE_AUX_JARS_PATH` env var indicating additional folders to include in the classpath
# Hadoop classpath
Hive uses Hadoop classpath. We can check which folders and jars it includes by running:
```
hadoop classpath
```
## HADOOP_CLASSPATH env var
The `HADOOP_CLASSPATH` environment variable can be used to add additional jars to the classpath used by Hadoop (i.e. used by Hive among the others). Hadoop builds its classpath from:
- Its own internal Hadoop jars
- Config directories (`HADOOP_CONF_DIR` env var)
- Anything listed in `HADOOP_CLASSPATH`

To add a folder with jar files to the Hadoop classpath, we can write:
```bash
export HADOOP_CLASSPATH=folder_with_jars/*:$HADOOP_CLASSPATH
```
# Hive lib folder
Usually the `/opt/hive/lib` folder is automatically included in the classpath when we use Hive's startup scripts.
# HIVE_AUX_JARS_PATH env var
The `HIVE_AUX_JARS_PATH` environment variable can be used to add additional jars to the classpath used by Hive.
# Testing jars using Hadoop
Since Hive uses all the jars included in the Hadoop classpath, we can use Hadoop as well for testing those jars.

For example if we have a jar for connecting to a cloud object storage, we can test it by running:
```bash
hadoop fs -ls <object-storage-URL>
```
which uses Hadoop to list all the files from a given object storage. 

But we need to keep in mind that Hive uses also additional jars, different that those from the Hadoop classpath (for example from the `$HIVE_HOME/lib` folder). Also config files like `core-site.xml` have an impact on whether different commands work.

So even if something doesn't work with Hadoop, it might work with Hive since for Hive we can have additional jars included in the `$HIVE_HOME/lib` folder and it can use a different `core-site.xml` file.