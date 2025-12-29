Tags: [[__Data_Engineering]]

# Introduction
Here is a link showing how to install and configure dbt: [www.youtube.com](https://www.youtube.com/watch?v=1fY1A8SRflI&list=PLc2EZr8W2QIBegSYp4dEIMrfLj_cCJgYA&index=3).

What we need to do is (we need to execute all the below commands in the directory with the dbt project):
- create venv: py -m venv venv
- install python libraries in that venv:
	- pip install dbt-core
	- pip install dbt-sqlserver (here we need to chose a porper adapter depending on what database we are using)
- create .dbt folder in the user directory, for example in the C:\Users\<username>: mkdir $home/.dbt
- Initialize dbt using the 'dbt init' command and provide the following values when prompted:
	- database: sqlserver
	- host name: name of the sql server
	- port: 1433
	- user, password, database: For those value we can use the same values which we provided when creating a SQL db using Terraform and sql_db module from azure_terraform repository.
	- threads: 4 is recommended, but other value can be used as well.

The dbt init command at the end will create the profiles.yml file in the .dbt folder which specifies our dbt configuration. It will also create a new folder with the name of our specified project name. We need to modify the profiles.yml file manually at the end so it contains the following content:
![[2 - Images/dbt/Screenshot 1.png]]

Then we can run the 'dbt debug' command in the project folder in order to test if it is set up properly.

#DataEngineering 