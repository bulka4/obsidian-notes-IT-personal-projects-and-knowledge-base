Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
This is an example of how to use the `search_runs` function ([[MLflow - Searching runs|link]]) in MLflow.

Find the run ID for the latest run in a given experiment:
```python
def get_latest_run_id(experiment_name: str) -> str:
    """
    Returns the run ID of the most recent run in the given experiment.
    """
    # Get experiment object by name
    experiment = mlflow.get_experiment_by_name(experiment_name)
    if experiment is None:
        raise ValueError(f"Experiment '{experiment_name}' not found")
    
    # Sort runs in descending order of start time
    runs = mlflow.search_runs(
        experiment_ids=[experiment.experiment_id],
        order_by=["start_time DESC"],
        max_results=1
    )
    
    if runs.empty:
        raise ValueError(f"No runs found in experiment '{experiment_name}'")
    
    # Return the run ID of the latest run
    return runs.loc[0, "run_id"]
```