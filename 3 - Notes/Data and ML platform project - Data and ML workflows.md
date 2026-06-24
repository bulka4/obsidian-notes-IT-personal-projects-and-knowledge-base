Tags: [[__My_projects]]
#MyProjects 

# Introduction
Below sections and documents describe how we can use this platform to create data and ML workflows.

In this project, we created one example workflow (more info about it here - [[Data and ML platform project - Example workflow|link]]). 

Next subsections describe what workflows we can create using this platform. It doesn't mean that all of that was implemented in the example workflow.
# Common code
In the `apps/common` folder we have a common code used by all other applications.
# Workflow orchestration with Airflow
Document below describes how workflow orchestration with Airflow looks like on this platform:
- [[Data and ML platform project - Airflow - How to build workflows]]
- [[Data and ML platform project - Workflows orchestrated by Airflow]]
	- [[Data and ML platform project - dbt with Airflow]]
	- [[Data and ML platform project - Making and saving predictions - Airflow orchestration]]
	- [[Data and ML platform project - Automatic update of ML models based on their performance]]
# Data transformation
Documents about data transformation:
- [[Data and ML platform project - Data transformation - Code and practices followed]]
	- [[Data and ML platform project - dbt folder structure]]
- [[Data and ML platform project - Data transformation - Running dbt (dev, kind)]]
- [[Data and ML platform project - Data transformation - Running Spark jobs]]
- [[Data and ML platform project - Data Transformation - Running SQL queries using Thrift server and Beeline]]
# Data ingestion
This document describes how we can perform data ingestion - [[Data and ML platform project - Data ingestion]]
# MLOps with MLflow
MLOps consists of:
- ML model training
- Performance monitoring
- Updating the model used in production with a new one when performance drops

More info about this workflow using MLflow on this platform can be found in documents below:
- [[Data and ML platform project - MLOps with MLflow]]
	- [[Data and ML platform project - Training, evaluating and saving ML models with MLflow]]
	- [[Data and ML platform project - Making and saving predictions]]
	- [[Data and ML platform project - ML model performance monitoring]]
	- [[Data and ML platform project - Automatic update of ML models based on their performance]]
# Monitoring
This document describes what we can monitor and how:
- [[Data and ML platform project - Monitoring]]