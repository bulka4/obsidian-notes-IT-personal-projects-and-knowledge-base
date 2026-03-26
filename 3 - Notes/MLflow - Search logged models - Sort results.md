Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
When searching through logged models using the `search_logged_models` function in MLflow, we can sort results.

For example, to find the model with the best metrics:
```python
best_models = mlflow.search_logged_models(
    experiment_ids=["1"],
    order_by=[
        {"field_name": "metrics.accuracy", "ascending": False}  # Highest accuracy first
    ]
)
```
# Example applications
Sorting runs can be used for example to:
- Find URI of the latest created model - [[MLflow - Find URI of the latest created model|link]] 