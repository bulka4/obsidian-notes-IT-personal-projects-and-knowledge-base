Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
When searching through runs using the `search_runs` function in MLflow, we can sort results.

For example, to find the latest run:
```python
runs = mlflow.search_runs(
	experiment_ids=[experiment_id],
	order_by=["start_time DESC"]
)
```
# Example applications
Sorting runs can be used for example to:
- Find ID of the latest run - [[MLflow - Searching runs examples - Find ID of the latest run|link]] 
- Find ID of the run with the highest / lowest metrics - [[MLflow - Searching runs examples - Find ID of the run with the highest or lowest metrics|link]] 