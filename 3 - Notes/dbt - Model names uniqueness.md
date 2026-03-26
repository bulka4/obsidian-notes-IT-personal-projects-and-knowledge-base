Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
In dbt, all the models (SQL scripts we have in the `models` folder) needs to have a unique name. 
# Model name case insensitiveness
Checking uniqueness of names is case-insensitive, so models like `modelName` and `modelname` will be treated as the same model.

We should avoid using names like `modelName` because that causes errors (dbt will say that there are two models `modelName` and `modelname`).
# Good practices
It is good to use names for models like `schema_name_model_name.sql`. This makes sure that there are no problems:
- When using names like `modelName` 
- If we want to create tables with the same names in different schemas (we can't create two models called `table_name.sql` but we can have `schema_1_table_name.sql` and `schema_2_table_name.sql`).