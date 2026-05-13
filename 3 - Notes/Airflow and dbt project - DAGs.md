Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
We have here two dags:
- dbt_dag.py
- dbt_task_group.py

The dbt_dag dag creates the entire dag just for perfmorming data transformations using dbt.

The dbt_task_group dag creates a task group for perfmorming data transformations using dbt. We can use that if we want to have additional activities in our dag except for dbt.