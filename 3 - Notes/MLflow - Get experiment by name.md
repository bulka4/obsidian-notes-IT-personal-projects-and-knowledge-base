Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
Find experiment based on its name:
```python
experiment = mlflow.get_experiment_by_name(experiment_name)
experiment_id = experiment.experiment_id
```
