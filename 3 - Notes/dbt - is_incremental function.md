Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
The `is_incremental()` function is used in a model and it returns true if and only if the model runs in the incremental mode ([[dbt - Incremental build of tables|link]]) and the table it builds already exists.

This is useful for example when we want to build a table called `table_name` and:
- Select rows which already exists in the `table_name` table, if that table exist
- Otherwise, select rows from another table
- Append those rows to the table we are building

So for example we can write:
```SQL
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
here `{{ this }}` refers to the table we are building, as also described here - [[dbt - The '{{ this }}' variable (referring the table which is currently being built)|link]].