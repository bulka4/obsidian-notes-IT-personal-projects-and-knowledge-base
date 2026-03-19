Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
This command:
```python
from mlflow.tracking import MlflowClient
client = MlflowClient()
client.list_artifacts(run_id)
```
shows saved artifacts ([[MLflow - Save artifacts|link]]) for a given run (but not models, to show models we need to use the `search_logged_models` function ([[MLflow - Searching logged models|link]])).