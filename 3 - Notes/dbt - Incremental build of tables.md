Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
In dbt tables can be build incrementally. Below sections describe different options of incremental build.
# Append all records from the source
If we write code like this:
```sql
{{ config(materialized='incremental') }}

select * from my_source
```
then it will append all the rows returned by the select statement to the target table.
# Merge / upsert (update existing rows, insert new rows)
Another option of an incremental build is merge / upsert. In this option we select rows from a source table and for each row:
- If the row doesn't exist in the target table yet, then insert it into the target table 
- If the row already exists in the target table, then update that row in the target table with new value from the source

We need to provide a column name which has unique values and can be used to determine whether or not a given row already exists in the target table.

For example this code:
```sql
{{ config(
    materialized='incremental',
    unique_key='id',
    incremental_strategy='merge'
) }}

select * from my_source
```
we use the `id` column to determine whether or not a given row already exists in the target table.
# Delete records which has been deleted in the source
If we want to additionally delete records in the target table which has been deleted in the source table, we have two options.
## Post-hook
We can use post-hook ([[dbt - post-hook|link]]) to delete records after performing merge (inserting new records and updating existing ones):
```sql
{{ config(
    materialized='incremental',
    unique_key='id',
    incremental_strategy='merge',
    post_hook="""
        DELETE FROM {{ this }}
        WHERE NOT EXISTS (
            SELECT 1
            FROM my_source s
            WHERE s.id = {{ this }}.id
        )
    """
) }}

select * from my_source
```
## Use database functionality
If our database which we use with dbt supports performing merge with deleting records, we can use it.

For example Iceberg ([[_Iceberg|link]]) provides such a functionality and we can use it in our model like that:
```sql
{{ config(alias="table_name") }}

MERGE INTO target_schema_name.target_table_name t
USING source_schema_name.source_table_name s
ON t.customer_id = s.customer_id
WHEN MATCHED THEN UPDATE SET *
WHEN NOT MATCHED THEN INSERT *
WHEN NOT MATCHED BY SOURCE THEN DELETE
```
