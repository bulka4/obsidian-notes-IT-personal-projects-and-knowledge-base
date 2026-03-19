Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
In dbt we can't combine SQL with Python, such that part of calculations in a single dbt model is done using SQL and the other part using Python, but there are ways to trigger a Python script from dbt. 

That Python script becomes another model which is run together with other, standard SQL models.
# dbt Python models
Tools like:
- Snowflake
- Databricks
- BigQuery
supports such an option that we can define a Python function which creates an entire table and that becomes a dbt model, which dbt runs together with other SQL models.

So our dbt project can consist of models which uses only SQL or only Python.
# dbt Hooks / run-operation
Tools like:
- `on-run-start`
- `on-run-end`
- `pre-hook`
- `post-hook`
- `dbt run-operation`
can trigger a Python script but with dbt it is hard to monitor and retry those scripts. dbt is not good for orchestration of such jobs.

This triggered script can't be integrated with a dbt SQL model, so we can't for example in a single dbt model perform part of calculations using SQL and other part using triggered Python script.

Triggered Python script becomes a separate, single job.