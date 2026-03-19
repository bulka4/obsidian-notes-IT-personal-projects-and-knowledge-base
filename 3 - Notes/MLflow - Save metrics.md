Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
We can assign metrics to a run, for example regarding model performance, like that:
```python
# Evaluate the model
y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

# set up the experiment
mlflow.set_experiment("linear_regression_eval")

# Start a run and assign metrics to it
with mlflow.start_run() as run:
    mlflow.log_metric("mse", mse)
    mlflow.log_metric("r2", r2)
```
# Find runs with the best metrics
We can also search through runs and find those with the best metrics like explained here - [[MLflow - Searching runs examples - Find ID of the run with the highest or lowest metrics]].