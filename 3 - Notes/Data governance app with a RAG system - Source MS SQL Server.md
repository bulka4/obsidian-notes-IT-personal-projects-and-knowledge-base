Tags: [[__My_projects]]
#MyProjects 

# Introduction
As a part of this project, we deploy on Kubernetes our own MS SQL Server from which we collect metadata and for which we create documentation in the data governance app.

When deploying this SQL Server, we also create on it sample data and scripts automatically.
# SQL Server initialization (sample data preparation)
When starting a SQL server by installing the Helm chart, we initialize it - i.e. we create on it a few sample tables, views and stored procedures for which we will be able to create documentation.

Initialization works like this:
- Install the Helm chart
- MS SQL Server is started
- Kubernetes Job runs a bash script which:
	- Connects to the deployed MS SQL Server
	- Waits until the MS SQL Server is ready
	- Runs on it a SQL script that creates sample tables, views and procedures
# Running SQL queries
In order to run SQL queries on this SQL Server, we can use the `k8s/ms_sql_test.yaml` manifest:
- Create a pod with the `sqlcmd` tool available - `kubectl apply -f k8s/ms_sql_test.yaml`
- Start interactive shell in the pod - `kubectl -n source-db exec -it mssql-tools -- /bin/bash`
- Run a query using this command: `sqlcmd -S mssql -U sa -P "$SA_PASSWORD" -Q "SELECT 1"`