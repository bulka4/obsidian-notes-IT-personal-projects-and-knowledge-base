Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
To get info about registered models we can use:
```python
client.search_model_versions(f"name='{model_name}'")
```

That returns a list of objects with properties like:
- `version`
- `stage`
- `run_id` - run that created the model
- `name` - model name

We can access those properties using:
```python
model_info = models_info[0]
model_info.version
```
# Latest model versions
To get ingo about latest versions of models per stage we can use function:
```python
models_info = mlflow.MlflowClient().get_latest_versions(name=model_name)
```

Or to get the latest version for specific stages:
```python
models_info = mlflow.MlflowClient().get_latest_versions(
    name=model_name,
    stages=[model_stage]
)
```
