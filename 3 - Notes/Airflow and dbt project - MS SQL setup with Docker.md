Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
Before running the Airflow DAG we need to create a MS SQL server and prepare there databases, schemas and tables with data which dbt will use for performing data transformations. It will be created using the 'mssql' service in the docker-compose.yml and the dockerfiles/mssql/Dockerfile.mssql file.

We need to create the Dockerfile.mssql file. For that we can use the Dockerfile-draft.mssql file, which is a draft of the Dockerfile we need to prepare. We need to provide there a password which will be used for logging into the created MS SQL server. We assign that password to the SA_PASSWORD environment variable in the Dockerfile.

In the dockerfiles/mssql folder we have two scripts needed for setting up a SQL server:
- **init.sql** - SQL script which will be executed on the created MS SQL server to create needed databases, schemas and tables with data which dbt will use to perform transformations.
- **sql_server_start.sh** - Bash script starting the MS SQL server and executing the init.sql script.