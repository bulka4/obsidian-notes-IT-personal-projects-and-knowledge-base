Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
To assign a run to a specific experiment, we can specify an experiment either in the `mlflow run` command:
```bash
mlflow run . --experiment_name={experiment_name}
```
or in the Python script:
```Python
mlflow.set_experiment("linear_regression")
```