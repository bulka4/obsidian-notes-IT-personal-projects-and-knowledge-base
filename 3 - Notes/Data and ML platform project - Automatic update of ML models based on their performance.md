Tags: [[_My_projects]]
#MyProjects 

# Introduction
The `update_model` Airflow DAG performs an automatic update of the ML model based on metrics about its performance saved in the Iceberg catalog prepared by dbt (model performance, prediction behavior, data drift) (more info here - [[Data and ML platform project - ML model performance monitoring|link]]).

In this DAG we:
- Check the performance of the current model using metrics saved in the Iceberg catalog (we do this in a new pod because it requires to prepare an environment properly with Spark)
- Based on the metrics decide whether or not the model requires retraining (we compare metrics values to some established threshold values)
- If specified conditions are satisfied, then using the Kubernetes Python start new pods and run in them:
	- MLflow project entrypoints to train new models
	- MLflow project entrypoints to evaluate all the models (new ones and old ones on new data as well)
	- Python script which uses MLflow to pick up the model with the best metrics and replace the model in the MLflow registry which is currently used in production with the new one
# Checking model performance task
The Airflow task for checking model performance is done in a new Kubernetes pod because we read metrics from the Iceberg catalog and that requires to prepare an environment properly with Spark.

Termination logs of the pod running the script in this task are used to determine whether or not the model requires an update.

We continue with further tasks in the Airflow DAG only when metrics are below established threshold.