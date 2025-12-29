Tags: [[__Cloud]], [[__Machine_Learning_Engineering]], [[__Distributed_computing]], [[__Data_Engineering]], [[_Databricks]]

# Introduction
We can keep here our files. There are so called containers:
![[2 - Images/Databricks - tutorial/Screenshot 3.png]]

In each container we can create folders and upload files.

 In order to access those files in databricks notebooks we need to write this code:
```
spark.conf.set(
    "fs.azure.account.key.<storage account name>.dfs.core.windows.net",
    "<access key to a storage account>"
)
```

And after that we can read data from Azure Data Lake by running for example this command:
```
spark.read.csv("abfss://<container name>@<storage account name>.dfs.core.windows.net/<path to csv file>")
```

#Cloud #MLEngineering #DistributedComputing #DataEngineering 