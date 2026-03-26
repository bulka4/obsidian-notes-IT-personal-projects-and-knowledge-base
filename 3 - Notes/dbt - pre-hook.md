Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
A pre-hook allows us to execute a command before building a model, for example we can create a table if it doesn't exist before we select data from this table:
```sql
{{ config(
    materialized='table',
    pre_hook="create table if not exists {{ this }} as select 1 as dummy"
) }}

select *
from {{ source('my_schema','my_table') }}
```
