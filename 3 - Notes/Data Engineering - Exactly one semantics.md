Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
In Data Engineering, we need to handle:
- duplicates
- retries
- idempotency
- deduplication
- transactional writes

especially in streaming systems.

For example, we can have a duplicate in the source data we are using or we might process the same record twice (e.g. ingest it from another source twice).