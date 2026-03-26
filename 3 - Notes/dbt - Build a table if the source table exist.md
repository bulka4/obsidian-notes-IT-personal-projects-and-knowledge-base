Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
When we want to build a table conditionally, only when the source table, used for building this table, exists, we have a few options for how to do this, described below.
# Use pre-hook
Using pre-hook we can pre-create the source table before we build the table which uses its data. Created source table will contain dummy data:
```sql
{{ config(
    materialized='table',
    pre_hook="create table if not exists {{ this }} as select 1 as dummy"
) }}

select *
from {{ source('my_schema','my_table') }}
```
# Using get_relation function
We can use the `get_relation` function to check whether the source table exist and then build the table using the condition:
- Build the table normally if the source table exists
- Build another dummy table if the source table doesn't exist
```sql
{{ config(...) }}

{% if not execute %}
  -- This block only runs at compilation, so safe to check
{% endif %}

{% set table_exists = adapter.get_relation(
    database='my_db',
    schema='my_schema',
    identifier='my_table'
) is not none %}

{% if table_exists %}
    select *
    from {{ source('my_schema', 'my_table') }}
{% else %}
    select null as placeholder
{% endif %}
```
## Incremental build
If we use an incremental build ([[dbt - Incremental build of tables|link]]), then we can still use the method with the `get_relation` function but our query should return 0 rows when the source table doesn't exist, to avoid adding repeatedly rows into the target table:
```sql
{{ config(materialize='incremental') }}

{% if not execute %}
  -- This block only runs at compilation, so safe to check
{% endif %}

{% set table_exists = adapter.get_relation(
    database='my_db',
    schema='my_schema',
    identifier='my_table'
) is not none %}

{% if table_exists %}
    select *
    from {{ source('my_schema', 'my_table') }}
{% else %}
    select null as placeholder
    where false
{% endif %}
```