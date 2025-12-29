Tags: [[__Cloud]], [[__Machine_Learning_Engineering]], [[__Distributed_computing]], [[__Data_Engineering]], [[_Databricks]]

# Introduction
We can use the Auto Loader (spark.readStream() function) in order to read data incrementally from the source. New files will be processed automatically (once per defined period of time) as they arrive to a specified folder and no files will be processed twice.

This code is reading data once per 10 second from a folder containing csv files. So once per 10 sec it will check if in a given folder there are new csv files which were not processed yet. If there are such a files then this code will read data from them. The folder in which we will be looking for a new files is given by the path ‘csv_files_path’.

Then we are creating a delta table which contains data from those csv files and it will be saved in the Azure Data Lake, in the folder given by the path delta_tables_path:
```
streaming_df = (spark.readStream

    .format("cloudFiles")

.option("cloudFiles.format", "csv")

    .option("cloudFiles.schemaLocation", checkpoint_path)

    .load(csv_files_path)

)

write_stream = (streaming_df.writeStream

    .format("delta")

    .outputMode("append")

    .option("checkpointLocation", checkpoint_path)

    .trigger(processingTime = '10 seconds')

.start(delta_tables_path)
```
- .format("cloudFiles") informs that we are loading data from the cloud

- .option("cloudFiles.schemaLocation", checkpoint_path) is defining that we will be saving info about data schema in the folder with path checkpoint_path.

- .option("checkpointLocation", checkpoint_path) defines that in the checkpoint_path there will be saved data about which files were already processed so spark can progress from where it left off in case of failure. Thanks to that files also won't be processed twice.

- We can use either .trigger(availableNow=True) in order to load data only once or .trigger(processingTime = '10 seconds') in order to start loading data every 10 seconds

#Cloud #MLEngineering #DistributedComputing #DataEngineering 