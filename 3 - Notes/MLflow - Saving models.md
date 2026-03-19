Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
We can save a model using for example the `mlflow.sklearn.log_model` function:
```python
import mlflow

model = LinearRegression(
    fit_intercept=args.fit_intercept
    ,positive=args.positive
)

model.fit(X_train, y_train)

# We can use also 'name' argument instead of 'artifact_path'
mlflow.sklearn.log_model(model, artifact_path="model_name")
```

Model's name specified by the `artifact_path / name` argument can be used when loading a model.

Models and artifacts are saved there in the following structure:
```bash
|-- experiment_1_ID
	|-- run_1_ID
		|-- artifacts
		|-- metrics
		...
	|-- run_2_ID
	...
	|-- models
		|-- model_1_ID
		|-- model_2_ID
		...
|-- experiment_2_ID
...
```