Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
During ingesting data from external sources ([[Data Engineering - Data ingestion|link]]) we can test different things to ensure that the process works correctly, for example:
- Row count - Check how many rows we have ingested and compare it with values from other ingestion runs. If this number is significantly lower than usual, something might be wrong.
- File size - Similar to a row count.
- File validation - Checking whether a file is valid (can we read it, are delimiters consistent, is JSON valid etc.)
- Ingestion pipeline health checks
	- API response status (200 vs errors)
	- Retry counts
	- Latency / throughput
	- Time to ingest
- Metadata consistency checks - If data source provides metadata describing which data is older / newer, e.g. batch ID or date, we can check whether:
	- There is no missing data (e.g. usually there are batches for everyday and for one day it was skipped or there are batch IDs increasing monotonically like 1,2,3, ... and there is one missing)
	- No “future” or very old data
- Latency
	- How much time the entire ingestion process takes
	- How much time we wait for the API response
- Throughput
	- How many rows / MB / events / files per second we transfer

# Questions
- 