Tags: [[__Machine_Learning_Engineering]]

# Introduction
We can load a model using an experiment and run ID:
```python
def load_model(experiment_ids, run_id):
    models = client.search_logged_models(experiment_ids=experiment_ids)
    for model in models:
        if model.source_run_id == run_id:
            model_id = model.model_id
            model = mlflow.sklearn.load_model(f"models:/{model_id}")
            
            return model

model = load_model(experiment_ids=["0"], run_id="a057c75c072e4162b870a3f6ceeb60e6")
```
- To get run ID, we need to search runs and we can get for example run ID of the latest run as described here - [[MLflow - Searching runs|link]].
- To get experiment ID, we need to search through experiments and for example find an experiment based on its name as described here - [[MLflow - Searching experiments|link]].
# Other methods to test
We can load models we logged ([[MLflow - Saving models|link]]) using for example this command:
```python
mlflow.sklearn.load_model(model_uri)
```
where `model_uri` can be one of two formats:
```python
runs:/{run_id}/{model_name}
models:/{model_name}/{model_version}
```

To get run id, we need to search through runs as described here - [[MLflow - Searching runs|link]]. For example, we can get a run ID of the latest run from a given experiment.

#MLEngineering 