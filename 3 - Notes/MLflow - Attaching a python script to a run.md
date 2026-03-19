Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
When we run a MLflow project using the `mlflow run` command, then it starts a run automatically but our Python script which we run as a part of this project doesn't have access to this run, so we can't for example get ID of that run or ID of the experiment:
```python
experiment_id = mlflow.active_run().info.experiment_id
run_id = mlflow.active_run().info.run_id
```
and if we log models or artifacts:
```python
mlflow.log_metric("mse", mse)
mlflow.sklearn.log_model(model)
```
they will not be associated with that run.

In order to attach our Python script to the run, we need to use `mlflow.start_run()`:
```python
with mlflow.start_run() as run:
	mlflow.log_metric("mse", mse)
	mlflow.sklearn.log_model(model)
```

The `mlflow.start_run()` function can start a new run if it was not started yet (if we run our script using `python script.py` instead of `mlflow run`) or attach our script to the current run where this script runs.

If our script is not attached to a run, then we can have problems such that:
- When we search logged models using `search_logged_models` ([[MLflow - Searching logged models|link]]) we might not see the `source_run_id` assigned to the model. Because of that we can have a problem with finding that model because we will not be able to find the model for a specific run ID.
- We will not see artifacts for that run using `list_artifacts` ([[MLflow - Listing artifacts|link]]).