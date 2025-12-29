Tags: [[__Cloud]], [[__Machine_Learning_Engineering]], [[__Distributed_computing]], [[__Data_Engineering]], [[_Databricks]]

# Introduction
Databricks secrets allow us to create secrets which contains json objects of the following format:
```
{
  "scope": string,
  "key": string,
  "string_value": string
}
```
We can for example create a secret which contains credentials needed to connect to Azure Data Lake. In order to do this we need to run those commands in databricks CLI:
```
- databricks secrets create-scope source_databases --initial-manage-principal users
- databricks secrets put-secret --json '{
  "scope": "source_databases",
  "key": "<storage account name>",
  "string_value": "<access key to a storage account>"
}'
```

After running those commands we can connect to Azure Data Lake by running this code in notebook:
```
spark.conf.set(
    "fs.azure.account.key.marcinstorage3.dfs.core.windows.net",
    dbutils.secrets.get(scope="source_databases", key="<storage account name>")
)
```
So the dbutils.secrets.get(scope, key) returns the ‘secret_value’ from our secret for given scope and key.

#Cloud #MLEngineering #DistributedComputing #DataEngineering 