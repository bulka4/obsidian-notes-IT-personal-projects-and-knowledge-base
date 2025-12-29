Tags: [[__Cloud]], [[__Machine_Learning_Engineering]], [[__Distributed_computing]], [[__Data_Engineering]]

# Introduction
When we create a managed table then we don’t specify where in an external storage that table’s data will be stored. Databricks will handle where to save this data for us.

If we drop a managed table then Databricks deletes the data saved in external location.

## Unmanaged tables (external tables)

When we create unmanaged table then we need to specify where in an external storage data of that table will be stored.

If we drop an unmanaged table then Databricks doesn’t delete the data saved in external location. Only the metadata is removed.

#Cloud #MLEngineering #DistributedComputing #DataEngineering 