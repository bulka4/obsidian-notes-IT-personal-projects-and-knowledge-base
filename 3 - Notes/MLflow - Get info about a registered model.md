Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
To get info about registered models we can use function:
```python
models_info = mlflow.MlflowClient().get_latest_versions(
    name=model_name,
    stages=[model_stage]
)
```

That returns a list of objects with properties like:
- `version`
- `run_id`

We can access those properties using:
```python
model_info = models_info[0]
model_info.version
```