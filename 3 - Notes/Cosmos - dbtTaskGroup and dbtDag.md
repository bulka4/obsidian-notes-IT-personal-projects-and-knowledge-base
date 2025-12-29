Tags: [[__Data_Engineering]]

# Introduction
The cosmos.dbtDag function creates the entire Airflow DAG for our dbt project.

The cosmos.dbtTaskGroup function create a task group in Airflow DAG for our dbt project.

## ProfileConfig

We need to create the ProfileConfig object where we provide path to the profiles.yml file and specifying the target:
![[2 - Images/dbt/Screenshot 5.png]]

Then we are using this profile config object in the dbtTaskGroup or dbtDag functions:
```
DbtTaskGroup(
	profile_config=profile_config
)
```

#DataEngineering 