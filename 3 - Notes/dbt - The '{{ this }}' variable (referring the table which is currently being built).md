Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
Using `{{ this }}` variable in a dbt model we can refer to the table which is currently being built by this model.

For example, using the incremental mode ([[dbt - Incremental build of tables|link]]) and the `is_incremental()` function ([[dbt - is_incremental function|link]]), we can:
- Select rows which already exists in the table we are building, if that table exist
- Otherwise, select rows from another table
- Append those rows to the table we are building:
```sql
{{ config(
    alias="table_name"
    ,materialized="incremental"
) }}

-- Select data from the "table_name" table which we are creating only if it already exists.
{% if is_incremental() %}
	(select col from {{ this }})
{% else %}
	(select col from {{ ref('another_table') }}
{% endif %}
```