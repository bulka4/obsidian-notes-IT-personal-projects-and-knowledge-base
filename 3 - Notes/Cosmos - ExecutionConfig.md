Tags: [[__Data_Engineering]]

# Introduction
We need to create the ExecutionConfig object where we provide a path to the dbt executable.

It is a good practice to create a virtual environment for dbt, install there all the dbt libraries needed (dbt-core, dbt-databricks) and provide the following executable path:

![[2 - Images/dbt/Screenshot 7.png]]

And pass it to the dbtTaskGroup or dbtDag:
```
DbtTaskGroup(
	execution_config=execution_config
)
```

This way dbt libraries will be kept separate to other libraries used by Airflow what is beneficial as those libraries might be in conflict.

#DataEngineering 