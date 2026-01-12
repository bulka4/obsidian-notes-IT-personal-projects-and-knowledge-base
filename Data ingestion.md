Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
Data ingestion is a process of transferring data from one data storage to another (called source to target data storage).

There are two types of data ingestion when it comes to frequency of transferring data:
- Batch - Transfer data with a constant frequency (e.g. every 5h)
- Streaming - Transfer new data immediately as it appears in the source

And there are two strategies for loading data in a batch ingestion:
- Full truncate and load - Remove all the data from the target data storage and load all the data from the source
- Incremental load - Detect what changes were made in the source data storage since the last transfer and transfer only those changes