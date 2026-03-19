Tags: [[_My_projects]]
#MyProjects 

# Experiments
- Each experiment corresponds to a specific goal, like predicting a revenue.
- Each run in an experiment is either building a model or evaluating it
- There can be different kinds of models taking different inputs in a single experiment
# MLflow projects
- Each MLflow project contains code for building and evaluating one specific kind of model, taking specific features as an input
- Models logged by each project needs to contain information about from which project they come from (so we can evaluate only them)
- Evaluating script evaluates models from this project. Models from different projects will require different evaluation techniques as they can take different features as an input.
- Evaluating script can evaluate:
	- All the models after a specified date
	- All models
	- The latest model
	- Models with specific parameters, tags, names
# Runs
- Evaluating runs - Each run for evaluating a model, evaluates only one model and logs:
	- metrics
	- URI of the evaluated model
	- ID of the run where the evaluated model has been built
# Promoting a model
To promote a model, i.e. save it in a MLflow registry, we use the `promote_model.py` script which finds URI of the model with the best performance.

This script finds the model with the best performance by searching through runs which were:
- Evaluating models
- Saving evaluation metrics and URIs of evaluated models
and picks a URI of the model with the best metrics.
# Code
More notes about MLflow projects code - [[Data and ML platform project - Code - MLflow projects]].
# Running MLflow projects and developing code
To run MLflow projects, we have two options:
- Use Helm chart
- Use development pod and connect to it with VS Code

Both options are described in sections below.
## Running MLflow projects using Helm chart
We can use the `helm_charts/mlflow_project` Helm chart to run MLflow projects which creates ML models:
```bash
# Run this command in the helm_charts/mlflow_project folder
helm -n mlflow install lr-model . &
```
## Running MLflow projects and developing code using dev pod and attaching to it VS code
Notes about how we can develop and run MLflow code by creating a dev pod and attaching VS Code to it - [[Data and ML platform project - Code development & testing scripts]].