Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
To get a run ID in a script we run using MLflow, we can either use the `start_run()` function:
```python
with mlflow.start_run() as run:
    # Get current experiment name
    exp_id = mlflow.active_run().info.experiment_id
    experiment_name = mlflow.get_experiment(exp_id).name
```
or get it from an env var:
```python
import os
run_id = os.environ["MLFLOW_RUN_ID"]
```
