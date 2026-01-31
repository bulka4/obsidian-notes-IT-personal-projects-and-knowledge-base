Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
When we save data using df.write, then Spark always saves this data as set of files in a folder.

So folder represents a table and each time we append data to that table using df.write, we create a new file in that folder.
### Data partitioning
When we want to save a big dataframe in a file using df.write, then Spark might split this table into multiple files.
### Data corruption
If we have already saved a table, that is a folder consisting of mutiple files, and then we try to add more that to that folder which have different columns and data types, it will work.

We will create a new file which have different columns and data types than other files in that folder creating a table and that will cause problems. If we want to read data from that table after that we might not be able to do that.

That’s why it is recommended to use additional tools which can prevent that, for example Delta lake.
