Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
Data pipelines can use a contract which describes how data should look like so those pipelines work correctly.

Thanks to that, pipelines depend on agreed data rules instead of implementation details of those pipelines.

Contract describes:
- Schema (column names, data types etc.)
- Data quality (no nulls, values in valid ranged etc.)
# Implementation
Below is described how to implement contract-based pipelines.
## 1. Schema enforcement
- One pipeline writes data into a table
- Another pipeline reads data from it
- Table schema enforces columns names and types, writing data which violates it will fail
## 2. Data validation checks
A pipeline's code checks data before using it. Pipeline fails if the check fails.