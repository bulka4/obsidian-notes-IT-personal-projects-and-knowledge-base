Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes how do we make predictions using ML models and save those predictions in the Iceberg catalog.
# A separate table for saving predictions
We run Python scripts orchestrated by Airflow which makes predictions using ML models and save them in a separate table that can be joined with other table which those predictions refer to.

For example one dimension table about clients can have columns:
```
clientID | country | industry
```
 and predictions will be saved in a separate table with columns:
```
clientID | predictedRevenue12m | timestamp | modelID
```
with a predicted revenue for the next 12 months.

The `timestamp` and `modelID` columns indicates which model made the prediction and when.
# Tools used
We use:
- MLflow - To load a model from a MLflow registry using model name and version, and to make predictions with it
- PyHive - To load data from the Iceberg catalog, used to make predictions
- Spark - To save predictions in an Iceberg table
## Improvements
As an improvement, we can use PyIceberg to load and save data in the Iceberg catalog. Docker image which we use will be then much smaller (Spark takes a lot of disk space) and we don't need to mount Spark config files.
# Orchestration with Airflow
We have an Airflow DAG which makes predictions and saves them.
# Testing code
For testing this process we can use two scripts:
- `/apps/test/make_predictions_spark_operator.py` - to be run with Spark Operator
- `/apps/test/make_predictions.py` - to be run without Spark Operator, using Python

Both scripts:
- Loads data from the Iceberg catalog by connecting to the Spark Thrift Server
- Loads a model from MLflow registry
- Makes predictions with it
- Saves predictions using Spark in the Iceberg catalog (not using the Thrift Server but it starts a new Spark driver)

How to run them is described in this document in the 'Make and save predictions' section - [[Data and ML platform project - Using the platform guide]].