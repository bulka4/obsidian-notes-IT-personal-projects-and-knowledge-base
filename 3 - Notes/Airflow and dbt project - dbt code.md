Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
dbt project with code which we will be executing in Airflow is in the dbt folder. We have defined there models, snapshots (as YAML files) and macros.
# dbt project configuration
We need to add the profiles.yml file to the dbt/data_warehouse folder where we specify the database in which we will be performing data transformations. For creating that file we can use the dbt/data_warehouse/profiles-draft.yml file which is a draft of the YAML file we need to prepare. We just need to provide there a password for connecting to the MS SQL server.

In that file we need to provide the password which will be used for connecting to the created MS SQL server. We set up that password in the Dockerfile what is described in the next section of this documentation 'MS SQL setup with Docker'.

In the profiles.yml file we are also specifying a name of the ODBC driver which dbt will use to connect to the MS SQL server. That is the driver which we were installing in Airflow containers as described in the 'ODBC driver installation' section of this documentation. 