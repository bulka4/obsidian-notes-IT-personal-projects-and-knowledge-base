Tags: [[__Data_Engineering]]

# Introduction
When running dbt we can select which nodes (models, snapshots) will be ran. More info about that: [docs.getdbt.com](https://docs.getdbt.com/reference/node-selection/methods).
# Selecting
When running dbt in a command line we are using it in the following way:
`Dbt run –select “pattern”`

For example this command will build all the snapshots:
`Dbt snapshot –select “snapshot:”`

And this will build a specific model:
`Dbt run –select “model_name”`

And this will run models with a specific tag:
`dbt run -s tag:my_tag`
## Select using multiple patterns
To run nodes matching all the patterns:
`dbt run -s pattern_1,pattern_2`

To run nodes matching one of the patterns:
`dbt run -s pattern_1 pattern_2`

For example `dbt run -s tag:tag_1,tag:tag_2`
# Excluding
In the same way we can use the `–exclude` option to exclude specific nodes from running.

#DataEngineering 