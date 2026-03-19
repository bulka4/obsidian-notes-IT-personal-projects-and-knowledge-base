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
# Running a dbt project
To run a dbt project we can use:
- Helm chart
- Airflow DAG

dbt will use code from the git repo, from the path `apps/dbt`, so we need to have that code uploaded to the repo.
## Helm chart
- We need to have Spark running (as described in the previous section)
- Install the chart:
```bash
# Run this command in the helm_charts/dbt folder
helm -n spark install dbt . &
```
- Connect to the dbt pod:
```bash
kubectl -n dbt exec -it dbt -- /bin/bash
```
- Run dbt project:
```bash
dbt run
```
## Airflow DAG
- Go to the Airflow UI at `localhost:8080`
- Trigger the dbt DAG from the Airflow UI
# dbt tags
We use dbt tags to group models based on different criteria:
- Data source
- Dimension and fact tables
## Data source group
Models have tags indicating from which source they use data.

For each data source, models which use its data are build together in a single run, right after data from that source has been ingested. 

Both data ingestion and running dbt models using this data is a single Airflow DAG.
# Simulating data from external sources
In the `dbt/workspace/models/source` folder we have folders with models which simulates data from external sources. Each folder corresponds to a single data source.
# Different data refreshing times
Tables have different refresh time, some of them are being updated daily while others are being updated weekly or monthly.

We update all the tables with the same refresh time by using tags (we run a single dbt run command and it builds all the tables with a specific tag which corresponds to a specific refresh time).
# dbt with Airflow
Notes about using dbt with Airflow are here - [[Data and ML platform project - dbt with Airflow]].