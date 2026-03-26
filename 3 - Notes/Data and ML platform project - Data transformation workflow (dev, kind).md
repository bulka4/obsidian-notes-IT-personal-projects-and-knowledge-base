Tags: [[_My_projects]]
#MyProjects 

# Running Spark Thrift Server
To run Spark Thrift Server we need to install the Helm chart:
```bash
# Run this command in the helm_charts/spark_thrift_server folder
helm -n spark install spark . &
```
## Running SQL queries with Beeline CLI tool
To query data we created in a Spark catalog, we can:
- Connect to the pod running Spark Thrift server:
  ```bash
  kubectl -n spark exec -it <pod-name> -- /bin/bash
  ```
  - Connect to Spark using Beeline:
    ```bash
    /opt/spark/bin/beeline -u jdbc:hive2://localhost:10000
    ```
- Then, we can run SQL queries
# Building tables with dbt
To build tables we need to run a dbt project. For that we can use:
- Helm chart
- Airflow DAG
## dbt files to run
dbt will use code from the git repo, from the path `apps/dbt` (it will be pulled when starting the pod), so we need to have that code uploaded to the repo.
## Dev pod
- We need to have Spark Thrift Server running (as described in the previous section)
- Install the chart:
```bash
# Run this command in the helm_charts/development_pods/dbt folder
helm -n spark install dbt . &
```
- Get access to a bash session in the created dbt pod:
```bash
kubectl -n dbt exec -it dbt -- /bin/bash
```
- Now we can run dbt commands in the pod.

That should create tables visible in Azure Data Lake. dbt connects to the Spark Thrift server in order to build those tables and they are created in the Iceberg catalog.
## Airflow DAG
- Go to the Airflow UI at `localhost:8080`
- Trigger the dbt DAG from the Airflow UI
