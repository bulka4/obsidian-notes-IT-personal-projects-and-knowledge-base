Tags: [[__Data_Engineering]] [[_Data_architecture]]
#DataEngineering #DataArchitecture  

# Introduction
We can structure data in a storage in such a way that we create layers, where:
- Each layer is a group of datasets with specific characteristics
- Data from one layer is used to create data in another layer
- Datasets in further layers are less universal (more specialized for specific needs)
# Layers
We can have for example the following layers:
## Source system
The first data layer contains a raw data from external sources. 

For example, it can consist of one database / schema per source system, called for example: 
- `01_System_1`
- `01_System_2`
## Transformed
The second layer contains a transformed data from the previous layer (from external systems). 

For example, like the previous layer, it can consist of one database / schema per source system.
## DWH (data warehouse)
The third layer contains data to be used for reports. Each dataset is prepared for a specific set of reports.

This layer can be divided into multiple groups, each one stored in a separate database / schema:
- **Common** – for common dimensions
- **Reference** – for reference data
- **Business function specific groups (data marts)** – for every business function (operations, finance etc) ([[Data Engineering - Data architecture - Data marts|link]])