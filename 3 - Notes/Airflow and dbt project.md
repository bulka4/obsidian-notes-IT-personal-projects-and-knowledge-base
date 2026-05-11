Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
This app is using Airflow and Astronomer Cosmos in order to run dbt code for performing data transformations in MS SQL server. 

In order to run the app we need to start Docker on our machine and run the command:
>`docker compose up`

That will run the Airflow app and also create and configure the MS SQL server.

In the below sections we can find a description of how this app works and what functionalities it provides.
# Apps code
- DAGs - [[Airflow and dbt project - DAGs]]
- dbt project - [[Airflow and dbt project - dbt code]]
# App prerequisites
Prerequisites we need to satisfy before we start using code from this repository - [[Airflow and dbt project - App prerequisites|link]].
# Infrastructure setup
- MS SQL setup with Docker - [[Airflow and dbt project - MS SQL setup with Docker|link]] 
- Airflow setup with Docker - [[Airflow and dbt project - Airflow setup with Docker|link]] 
# PowerShell scripts
In this repository, we have some useful PowerShell scripts - [[Airflow and dbt project - PowerShell scripts|link]].
# dbt with Airflow - materials
Materials about running dbt with Airflow:
- [www.astronomer.io](https://www.astronomer.io/docs/learn/airflow-dbt/) - Creating a task group.
- [astronomer.github.io](https://astronomer.github.io/astronomer-cosmos/getting_started/open-source.html) - Creating a dbt dag.
- [astronomer.github.io](https://astronomer.github.io/astronomer-cosmos/configuration/execution-config.html) - Configuration (for example creating execution_config).
- [astronomer.github.io](https://astronomer.github.io/astronomer-cosmos/profiles/index.html) - Creating profiles (creating profile_config).
- [youtube.com](https://www.youtube.com/watch?v=MhCuxTDlVkE) - video with overview of using Astronomer Cosmos framework for running dbt with Airflow.