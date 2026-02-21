Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
Here is a link showing how to install and configure dbt: [www.youtube.com](https://www.youtube.com/watch?v=1fY1A8SRflI&list=PLc2EZr8W2QIBegSYp4dEIMrfLj_cCJgYA&index=3).
# Initial setup
What we need to do is (we need to execute all the below commands in the directory with the dbt project):
- create venv: py -m venv venv
- install python libraries in that venv:
	- pip install dbt-core
	- pip install dbt-sqlserver (here we need to chose a porper adapter depending on what database we are using)
# Profiles.yaml
We need to prepare the `profiles.yaml` file in the `.dbt` folder in the user directory (for example `C:\Users\username`) which specifies our dbt configuration.
## dbt init
We can create it using the `dbt init` command:
- create .dbt folder in the user directory
- Initialize dbt using the 'dbt init' command and provide the following values when prompted:
	- database: sqlserver
	- host name: name of the sql server
	- port: 1433
	- user, password, database: For those value we can use the same values which we provided when creating a SQL db using Terraform and sql_db module from azure_terraform repository.
	- threads: 4 is recommended, but other value can be used as well.

`dbt init` also creates a new folder with the name of our specified project name where we will be creating new files for the project.
## Manual preparation
We can also prepare `profiles.yaml` by creating that file manually:
```yaml
profile_name:
  target: dev
  outputs:
	dev:
	  type: sqlserver
	  driver: "ODBC Driver 18 for SQL Server"
	  database: <your-database-name>
	  schema: <your-schema-name>
	  host: localhost (if we are running SQL server on the same host as dbt)
	  password: <your-password-to-SQL>
	  port: 1433 (port for connecting to the SQL server)
	  threads: <number-of-threads>
	  type: sqlserver
	  user: <username> (username for accessing SQL server)
	  encrypt: true
	  trust_cert: true
```
## Testing
We can run the `dbt debug` command in the project folder in order to test if the `profiles.yaml` is set up properly.
# Project setup
Folder structure:
```bash
my_dbt_project/
|-- dbt_project.yml
|-- models/
	|-- model.sql
```
## Project file
dbt_project.yml:
```yaml
name: 'my_dbt_project'
version: '1.0'
config-version: 2

profile: 'profile_name'

model-paths: ["models"]
target-path: "target"
clean-targets:
  - "target"
  - "dbt_modules"

```