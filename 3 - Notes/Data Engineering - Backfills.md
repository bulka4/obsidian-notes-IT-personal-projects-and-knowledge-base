Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
A backfill is re-running an incremental process only for a part of all the data available. That refers to incremental data ingestion and transformations.
# When it is needed
It is needed when:
- New data comes late for a batch (e.g. for a day) which we already processed 
- Data contained some errors which were fixed later, after we already processed this data.
# Backfill types
Below are explained different types of backfills we can perform.
## Partition-based backfills
If our table is partitioned (e.g. by `date`), we can recompute only selected partitions.

For example, if our table is partitioned by date:
```
date = 2026-04-10  
date = 2026-04-11  
date = 2026-04-12
```
we can recompute only:
- `WHERE date BETWEEN '2026-04-10' AND '2026-04-12'`

Then:
- Overwrite those partitions only
- Leave the rest untouched
### How it's implemented
For example, In Spark:

```python
df_backfill.write \  
  .mode("overwrite") \  
  .option("replaceWhere", "date >= '2026-04-10' AND date <= '2026-04-12'") \  
  .saveAsTable("target_table")
```
- Only those partitions get replaced  
- Entire table is not rewritten
## Merge / upsert (row-level backfill)
If our table isn’t strictly partitioned - or we need finer control we use MERGE (upsert).
### Idea
- Recompute affected rows
- Match on a key (e.g. `user_id`, `event_id`)
- Update only those rows
### Example

```sql
MERGE INTO target t  
USING backfill_data s  
ON t.id = s.id  
WHEN MATCHED THEN UPDATE SET *  
WHEN NOT MATCHED THEN INSERT *
```

This:
- Fixes incorrect rows
- Inserts missing ones
- Leaves everything else untouched
## Parameterized backfills
We can parametrize pipeline so we can run it for example for a specific time range:
```
run_pipeline(start_date, end_date)
```

So we can:
- Normal run → `start = yesterday`
- Backfill → `start = '2026-01-01', end = '2026-01-31'`

Then internally:
- Filter source data
- Overwrite only that range
# What makes this possible
We can only do efficient backfills if:

Our data is:
- Partitioned (by date, id range, etc.)
- Or keyed (for merges)

Our pipeline is:
- Deterministic (same input → same output)
- Idempotent (safe to re-run)

Otherwise we’re forced into full refreshes.
# Questions
- 