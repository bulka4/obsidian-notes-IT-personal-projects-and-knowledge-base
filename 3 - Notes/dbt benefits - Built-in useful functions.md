Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
dbt provides a lot of useful build-in functions, for example `is_incremental()`. It is useful when building a table in an incremental way.

For example, let's assume that we want to build a table called `table_name`. We can write a code like shown below, which:
- Selects rows which already exists in the `table_name` table, if that table exist
- Otherwise, selects rows from another table
- Appends those rows to the `table_name` table

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