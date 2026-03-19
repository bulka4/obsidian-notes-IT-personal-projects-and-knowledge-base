Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
We can search models we logged ([[MLflow - Saving models|link]]) using the `search_logged_models` function:
```python
from mlflow.tracking import MlflowClient

client = MlflowClient()
models = client.search_logged_models(experiment_ids=["1"])
```
It returns a list of logged models with information such as:
- `artifact_location`
- `creation_timestamp`
- `experiment_id`
- `model_uri`
- `name`
- `source_run_id`

