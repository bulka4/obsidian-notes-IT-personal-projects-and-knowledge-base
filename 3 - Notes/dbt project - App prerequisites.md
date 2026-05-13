Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Create a Dockerfile
We need to create a Dockerfile in the `mssql_preparation` folder and for that we can use the `mssql_preparation/Dockerfie-draft` file. 

The Dockerfile which we need to create looks exactly the same as the `Dockerfile-draft` but we need to assign there a chosen value to the `SA_PASSWORD` environment variable which will be a password which we will be using for connecting to the created MS SQL server. 

There will be automatically created a user with the 'sa' username. We need to use it together with our defined password in order to connect to the created SQL server.
# Install ODBC driver
We need to have installed the 'ODBC Driver 18 for SQL Server' on our computer. It is possible to use other driver as well and then we need to provide name of that driver in the `profiles.yml` file. 

More information about that can be found in the 'Prepare profiles.yml' section further in this documentation.
# Prepare venv
We need to create a venv and install all the required Python libraries in order to run dbt code. In order to do that we need to follow those steps:
```shell
#create venv
py -m venv venv
# Install libraries
pip install -r requirements.txt
```
# Prepare profiles.yml
In order to create this file we need to create at first the `.dbt` folder at `C:\Users\<username>` (on Windows). Then we need to run the `dbt init` command and provide the following values when prompted:
- database: sqlserver
- host name: name of the sql server
- port: 1433
- user, password, database: For those value we can use the same values which we provided when creating a SQL db using Terraform and `sql_db` module from `azure_terraform` repository ([github.com](https://github.com/bulka4/azure_terraform)).
- threads: 4 is recommended, but other value can be used as well.
 
After that we are gonna have created the `profiles.yml` file in the`.dbt` folder and we need to modify it a little bit. It needs to look like that:
```
data_warehouse:
  outputs:
    dev:
      type: sqlserver
      driver: "ODBC Driver 18 for SQL Server" # the ODBC driver which we want to use from our computer
      database: dwh
      schema: dbo
      host: localhost
      password: <your_password> # password from the Dockerfile
      port: 1433
      threads: 4
      type: sqlserver
      user: sa
      encrypt: true
      trust_cert: true
  target: dev
```

At the end we can run the `dbt debug` command to make sure everything works properly.