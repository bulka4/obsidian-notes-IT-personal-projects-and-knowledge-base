Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
We can add tags to dbt models:
```sql
{{ config(alias="table_name", tags=['tag_1', 'tag_2']) }}

select ...
```
