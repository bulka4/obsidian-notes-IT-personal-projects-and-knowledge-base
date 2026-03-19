Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
This is an example of how to use the `search_runs` function ([[MLflow - Searching runs|link]]) in MLflow.

We can log metrics for a run:
```python
# Evaluate the model
y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

# Set up the experiment
mlflow.set_experiment("linear_regression_eval")

# Start a run and assign the metrics to it
with mlflow.start_run() as run:
    mlflow.log_metric("mse", mse)
    mlflow.log_metric("r2", r2)
```
And find the run with the highest / lowest values of specific metrics:
```python
experiment = mlflow.get_experiment_by_name("linear_regression_eval")

# Sort runs on the mse metric in ascending order and on the r2 metric in descending order
runs = mlflow.search_runs(
	experiment_ids=[experiment.experiment_id],
	order_by=["metrics.mse ASC", "metrics.r2 DESC"],
	max_results=1
)
```
