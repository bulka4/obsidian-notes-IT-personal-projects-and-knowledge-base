Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Docker compose file
We use the original Docker compose file for Airflow (which we can get from here: [airflow.apache.org](https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html)) which we have modified slightly as described in sections below.
# Mounting dbt folder
We mount the dbt folder with our dbt project to Airflow containers by writing in the `docker-compose.yaml` file:
```yaml
x-airflow-common:
  ...
  volumes:
	  - ${AIRFLOW_PROJ_DIR:-.}/dbt:/opt/airflow/dbt'
```
# Dockerfile
We use our own Dockerfile `dockerfiles/airflow/Dockerfile.airflow` file for preparing Airflow containers. 

We specify to use that Dockerfile in the `docker-compose.yaml` file in the `x-airflow-common.build` field.
## ODBC driver installation
In the Dockerfile we install a ODBC driver which will be used by dbt to connect to the MS SQL server. 
## virtual environment for dbt
- In the Dockerfile we create a virtual environment where we install dbt. 
- We can specify which version of dbt we will use and which database adapters we want. 
- We create that virtual environment in order to make sure the dbt libraries will not be in conflict with Airflow libraries.

In the Airflow DAG, using the `ExecutionConfig` function, we specify as the executable path a path from that virtual environment. That means that Airflow in order to run dbt commands (like dbt run) will use dbt executables from that virtual environment. 
## Python libraries for Airflow DAGs
In the Dockerfile we install all the Python libraries which we want to use in our DAGs.

Those are libraries listed in the `dockerfiles/airflow/requirements.txt` file. It doesn't include dbt related libraries which will be installed in a virtual environment like described in the previous section 'virtual environment for dbt'.