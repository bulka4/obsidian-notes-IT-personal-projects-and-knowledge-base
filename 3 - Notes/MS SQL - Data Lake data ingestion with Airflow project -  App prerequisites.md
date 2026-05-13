Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Create an Azure MS SQL database and Azure Data Lake 
Between those databases we will be transferring data. For that, we can use the [azure_terraform](https://github.com/bulka4/azure_terraform) repository, `data_lake` and `sql_db` modules which will create all the Azure resources needed automatically using Terraform.
# Set up firewall rules in the SQL database
In order to connect to the created SQL database we need to add our IP address to the firewall rules. 

In order to do this:
- Go to the Azure platform
- Go to the MS SQL server resource
- Go to the `security > networking` section. 
	- Here we can add the IP address of our currently used computer to the firewall rules.
# Ingest data into the SQL db
We need to ingest data into the SQL db which we will be later on ingesting into the Data Lake using Airflow. 

We can do that using the `sql_ingestions_v1.py` script from the `data_lake_ingestion` repository ([github.com](https://github.com/bulka4/data_lake_data_ingestion)) which is using the `SQLAlchemy` library.
# Set up container in the Data Lake
We need to create a container and directory in the Data Lake into which we will be ingesting data. 

For that we can use the `data_lake_setup.py` script from the `data_lake_ingestion` repository ([github.com](https://github.com/bulka4/data_lake_data_ingestion)) repository which is using Azure SDK.
# create the .env file
- That file should be located in the `dags/project_1` folder together with the `data_ingestion_dag.py` script. 
- It should look like the `.env-draft` file in the same location. 
- It is described in that draft file what values to provide. 
- That file will contain confidential variables which are accessed in the `data_ingestion_dag.py` script using the `os.getenv()` function. 
	- They are needed for connecting to the SQL database and Data Lake.