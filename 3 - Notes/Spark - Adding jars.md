Tags: [[_Spark]] [[__Data_Engineering]], [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Introdcution
The `/opt/spark/jars` folder contains jars (Java libraries) which Spark uses to use different functionalities (they are added to the Spark's classpath ([[Java - Classpath|link]])).

If we want to add new jars to bring new functionalities to Spark, e.g. enable using Iceberg ([[_Iceberg|link]]), we need to add to this folder proper jars.
# spark.jars.packages
We can also use `spark.jars.packages` config to download jar when spark starts but that takes additional time and there is more issues with it.