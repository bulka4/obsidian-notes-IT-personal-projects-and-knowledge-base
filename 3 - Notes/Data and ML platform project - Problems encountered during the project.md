Tags: [[__My_projects]]
#MyProjects 

# Main problems
## Infrastructure
### Spark and dbt configuration for Iceberg catalog
It was complicated to configure Spark and dbt to use correctly Iceberg catalog and access Azure Data Lake.

I needed to create a schema called `default` in the Iceberg catalog before starting Spark Thrift Server because without it I was getting errors that this database doesn't exist.

Also, I couldn't create dynamic Spark configuration inside the Spark Operator YAML manifest. I needed to create them in the Spark application itself.
### Git-sync
I wanted to set up a pod running git-sync which would systematically pull code from a repo and save it in a volume that could be used by many pods.

I needed a volume which supports:
- RWS (mounting to pods on different nodes)
- POSIX permissions (allowing to set up file permissions) - because git-sync tries to automatically set up those permissions

There was a problem with finding a volume that would satisfy both.

As a workaround, I have:
- Used a volume which only supports RWX (Azure File share)
- Git-sync was running in one container, saving pulled code not in the Azure File share volume but in the ephemeral volume in the pod
- Another sidecar container in the same pod was copying pulled code from the ephemeral volume into the main one (Azure File share)

More about this - [[Git-sync - Kubernetes deployment]].
## Updating the model
I needed to create an Airflow DAG which:
- Checks metrics about model performance from an Iceberg table
- Based on read values, decides whether or not to continue with next, downstream tasks for training a new model

The problem was to create an Airflow task for checking metrics. It needed to:
- Run in a pod (so it has all the dependencies for the script)
- Return a value which can be read by another Airflow task

I have used for that pod termination logs. I created a custom Airflow operator such that:
- It creates a pod which runs a script for checking metrics
- The script saves metrics in pod's termination logs
- Operator waits for the pod to complete and reads termination logs 
- Operator returns a true or false value based by checking whether termination logs contain a specific key-value pair.
	- Returned true / false value is used to determine whether or not to progress with downstream tasks in the DAG
## dbt - Order of building tables
Table with predictions, was:
- In the middle of table dependency graph, so:
	- This table was depending on other tables built by dbt
	- This was needed to build other tables using dbt
- Created outside of dbt (by a Python script)

So I couldn't build all the dbt tables at once because:
- If I try to do this before the table with predictions is created, the dbt process will fail because some of the dbt tables are dependent on this table.
- I couldn't create at first the table with predictions and then build all the dbt tables because to make predictions I needed to prepare a part of the tables using dbt first

So I needed to:
- First build a part of dbt tables which are needed to make predictions
- Then make predictions and save them in the table
- Then build another part of dbt tables which were calculating metrics about those predictions

I have used tags to build different groups of tables with dbt.
# Others
## Infrastructure
### Hive Metastore
When setting up Hive Metastore, I had a problem to use it with Azure Data Lake. It looked like it was missing some JAVA libraries required to connect to it and work with files inside.

I was trying to provide those libraries but couldn't make it work when using the official Hive Docker image.

Finally, I needed to create a custom Docker image to make this work.

Also, I didn't realize that I can use only Iceberg without Hive at all. So I prepared Hive unnecessarily, but at least I have learnt about it.
### Airflow configuration
Airflow configuration was complicated, providing all the values in the `values.yaml` file for the Helm chart:
- I didn't include the `airflow:` at the top of this file, to specify that those are parameters for the dependency chart which is the official Airflow chart. Because of that, those parameters were not applied to the official Airflow chart. It took me quite a while to realize that this is the issue.
- Specifying a service account that Airflow needs to create pods
- When working on kind (local Kubernetes cluster running in Docker containers), I needed to use a `NodePort` service for the webserver, to access it from the local computer. 
	- It was quite tricky because it specifies port which can be used to access this service from the container running a kind Kubernetes cluster, not from the local computer.
	- I needed additionally to configure port mapping in the kind config, so that the traffic which goes to a specific port on the local host, goes to a specific port in the kind container
- I needed to create additional init container which creates Airflow connection to Azure Data Lake. I needed to provide there value for one of the environment variables used by Airflow `AIRFLOW__DATABASE__SQL_ALCHEMY_CONN` so that I can use Airflow command for creating a connection.
## Calculating metrics about model performance
When calculating metrics about model performance, I needed to make sure that:
- We consider only predictions made by the latest model
- When comparing predictions with real values (about revenue per month), we compare the same months
- We have metrics calculated for every month
	- In order to do this, the dbt model for calculating metrics needs to be ran every month
- Nothing wrong will happen if we run the model for calculating metrics and there are no predictions yet
	- I made the model this way so that it will not create any new, unnecessary records
## MLflow
### Deleting metadata
Deleting metadata was problematic. If I wanted to perform a hard to delete, to permanently delete for example an experiment so that I can create another one with the same name, I needed to run SQL queries to delete this data in the SQL database.

I needed to find all the tables containing the relevant information that I want to delete.
### Custom functions
I needed to prepare some custom functions, like:
- Finding the latest created model - So that I can evaluate only this one
- To find the model with the best metrics to use it in the production pipeline