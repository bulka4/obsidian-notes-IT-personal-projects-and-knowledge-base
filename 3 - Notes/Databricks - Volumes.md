Tags: [[__Cloud]], [[__Machine_Learning_Engineering]], [[__Distributed_computing]], [[__Data_Engineering]]

# Introduction
Volumes help with managing data (saved in for example ADLS).

We create volumes in Unity Catalog’s catalog / schema namespace: catalog.schema.volume_name.

Each volume refers to a folder in an external data storage. For example if we have a volume catalog.schema.volume1 which refers to folder1/folder2 in an external storage, then in order to access the folder1/folder2/folder3/file.csv file in databricks by using this path:
- /Volumes/catalog/schema/volume1/folder3/file.csv

Instead of a full path:
- folder1/folder2/folder3/file.csv

Volumes are available only when using Unity Catalog. We can also manage volumes like tables in Unity Catalog (permissions etc).

#Cloud #MLEngineering #DistributedComputing #DataEngineering 