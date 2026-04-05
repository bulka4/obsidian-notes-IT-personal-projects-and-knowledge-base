Tags: [[__MLOps]]
#MLOps 

# Introduction
To be able to reproduce a model ([[MLOps - Model reproducibility|link]]), we need to be able to reproduce the dataset which was used for training it.

To achieve that, we can use:
- Data versioning (time travel) - Saving info about all the changes that happened to a table. For example Iceberg provides such a functionality - [[Iceberg - Introduction|link]].
- Slowly changing dimension type 2 - Creating a dimension table with columns `valid_from` and `valid_to` indicating when given record was valid (if it changed). dbt has features making it easier to build dimension tables like that - [[dbt benefits - Slowly changing dimensions type 2|link]].