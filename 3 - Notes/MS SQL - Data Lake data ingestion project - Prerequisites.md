Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
Before we use that code we need to perform the following preparations:
- **Create an Azure SQL database and Azure Data Lake** - between which we will be transferring data. For that we can use the azure_terraform repository, data_lake and sql_db modules.
- **Set up firewall rules in the SQL database** - in order to connect to the created SQL database we need to add our IP address to the firewall rules. We can do that in Azure platform if we go to the MS SQL server resource > security > networking. There we can add the IP address of our currently used computer to the firewall rules.
- **Save credentials in the .env file** - We need to create the .env file which looks like the .env-draft file, in the same location. We specify there values for variables which we are accessing in the code using the os.getenv() function. In that draft file it is describe what values to provide.
- **Install ODBC driver** - We need to have installed a proper ODBC driver which will be used by the SQLAlchemy library to connect to the SQL db. The default and recommended one for Windows is the 'ODBC Driver 18 for SQL Server'. We can use a different driver and then we need to specify that driver when initiating the SQL class which we will be using.