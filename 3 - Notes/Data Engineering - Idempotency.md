Tags: [[__Data_Engineering]]
#DataEngineering 

## Definition
A pipeline is idempotent if running it multiple times produces the same result.
# Example
## Non-idempotent pipeline
- Load data for `2026-04-10`
- Append to table

If it runs twice → duplicated data.
## Idempotent pipeline
- Load data for `2026-04-10`
- Overwrite that partition

If it runs twice → same result.
# Problem it solves
- Task fails halfway
- We rerun it
- Now our data is duplicated or corrupted
# Useful techniques
- Upserts (MERGE INTO) ([[Data Engineering - Upsert (MERGE INTO)|link]])
- Partition-based writes (`date=...`) ([[Data Engineering - Partition-based writes|link]])
- Deduplication keys (a column that uniquely identify each record)
- Immutable raw layer ([[Data Engineering - Immutable raw layer|link]]) + deterministic transformations
## Upserts
Upserts give us idempotency directly because for the same input data, we will always obtain the same output no matter how many times we run the pipeline.
## Partition-based writes
Partition-based writes helps to obtain idempotency such that we can create a pipeline where we take data from a source and overwrite a specific partition in the target table with that data.

Thanks to partitioning, we don't need to overwrite the entire table which is faster.
## Deduplication keys
Deduplication keys are used to identify and remove duplicated records. They can be used to perform an upsert or to remove duplicated records after appending data.
## Immutable raw layer + deterministic transformations
Deterministic transformations are transformations which always give the same output for the same input. 

Together with an immutable raw layer ([[Data Engineering - Immutable raw layer|link]]) gives us idempotency because we always have available the same data which was used previously and deterministic transformations will give us the same results.