Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
Before we run this app we need to:
- **Install Docker** - which will be running our app in containers
- **Set up a password for MS SQL server** - We do that in the dockerfiles/mssql/Dockerfile.mssql file. More info below in the 'MS SQL setup with Docker' section. Also we need to add this password to the dbt/data_warehouse/profiles.yml file like described in the 'dbt project configuration' section below.