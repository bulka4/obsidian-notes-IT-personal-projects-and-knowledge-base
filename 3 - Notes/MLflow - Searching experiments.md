Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
We can use the `search_experiments` function to get information about experiments. It returns a list with experiment objects which contains information such as:
- `experiment_id`
- `name`
- `artifact_location`
- `creation_time`

We can use this to find experiment ID of our experiment and then use it to search runs for that experiment using the `search_runs` function ([[MLflow - Searching runs|link]]):
```python
def get_experiment_id(experiment_name):
	experiments = mlflow.search_experiments()
	for e in experiments:
		if (e.name == experiment_name)
			return e.experiment_id
```
# Get experiment by name
There is also a function to find experiment based on its name:
```python
experiment = mlflow.get_experiment_by_name(experiment_name)
experiment_id = experiment.experiment_id
```