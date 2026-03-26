Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
The post-hook functionality can be used to execute a SQL query after the main query from the model has been executed.

For example, after performing merge incremental build which inserts new records and update existing ones (more info about it here - [[dbt - Incremental build of tables|link]]), post-hook can delete records in the target table which has been deleted in the source table:
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