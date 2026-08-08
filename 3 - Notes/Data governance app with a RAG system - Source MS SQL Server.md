Tags: [[__My_projects]]
#MyProjects 

# Introduction
As a part of this project, we deploy on Kubernetes our own MS SQL Server from which we collect metadata and for which we create documentation in the data governance app.
# SQL Server initialization
When starting a SQL server by installing the Helm chart, we initialize it - i.e. we create on it a few sample tables, views and stored procedures for which we will be able to create documentation.

Initialization works like this:
- Install the Helm chart
- MS SQL Server is started
- Kubernetes Job runs a bash script which:
	- Connects to the deployed MS SQL Server
	- Waits until the MS SQL Server is ready
	- Runs on it a SQL script that creates sample tables, views and procedures