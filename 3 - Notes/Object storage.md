Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
In object storage we mange data as objects. Each object consists of:
- Data (like CSV file)
- Metadata
- A unique identifier (key, name of an object)

Objects are not stored like files in directories in buckets (containers). Each object is saved in a container and there are no nested containers (container saved in another container).

An object can be accessed by specifying a container and an object name (key):
- Container_name/folder1/file.csv

A name of an object can have slashes in it. So it looks like files saved in folders but in reality the /folder1/file.csv is a single object saved in the ‘container_name’ container.

#DataEngineering #DistributedComputing 