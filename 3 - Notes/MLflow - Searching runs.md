Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
We can use the `search_runs` function to get information about different runs. It returns a DataFrame with information about runs. It contains such a columns as:
- `run_id`
- `experiment_id`
- `artifact_uri`
- `status`
- `start_time` and `end_time`
- Tags
- Params
- Metrics
# Examples
In documents listed below we can find examples of how we can search through runs:
- Find ID of the latest run - [[MLflow - Searching runs examples - Find ID of the latest run|link]] 
- Find ID of the run with the highest / lowest metrics - [[MLflow - Searching runs examples - Find ID of the run with the highest or lowest metrics|link]] 