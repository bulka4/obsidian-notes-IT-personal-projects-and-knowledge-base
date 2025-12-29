Tags: [[__Data_Engineering]]

# Introduction
When running dbt we can select which nodes (models, snapshots) will be ran. More info about that: [docs.getdbt.com](https://docs.getdbt.com/reference/node-selection/methods).

When running dbt in a command line we are using it in the following way:

Dbt run –select “pattern”

For example this command will build all the snapshots:

Dbt snapshot –select “snapshot:”

And this will build a specific model:

Dbt run –select “model:model_name”.

**Excluding**

In the same way we can use the –exclude option to exclude specific nodes from running.

#DataEngineering 