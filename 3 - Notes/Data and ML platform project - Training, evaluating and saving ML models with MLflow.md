Tags: [[_My_projects]]
#MyProjects 

# Running and developing code
## Create a development pod
We can use development pods (more info here - [[Data and ML platform project - Code development & testing scripts|link]]) to develop and test MLflow code:
  ```bash
	# Run this from the helm_charts/development_pod/mlflow folder
	helm -n mlflow install dev-pod . &
  ```
## Mounted files
The `apps` folder from the host will be mounted to the created development pod. So we can edit code on the host and then run it from that pod.
## Get access to a bash session in the created pod
To get access to a bash session in the created pod so we can run commands we can:
- Attach VS Code to that pod like described here - [[Data and ML platform project - VS Code Kubernetes extension setup for code development|link]] 
  - Or use `exec -it dev-pod -- /bin/bash`
## Run MLflow projects
  Use files from the `/root/apps/mlflow_projects/linear_regression_revenue` folder to perform actions described below:
  - Use commands from the `run_script.bash` file:
	  - Run the command for training (we can create multiple models using different parameters `fit_intercept` and `positive`)
	  - Run the command for evaluating all the models
  - Run the `python3 promote_model.py` command to run the Python script which takes the best model (with the best metrics from the evaluation) and saves it in the MLflow registry
  - To delete an experiment / run, use the `delete_exp_run.py` script.
## Running MLflow projects using Helm chart
We can use the `helm_charts/mlflow_project` Helm chart to run MLflow projects which trains and evaluates ML models:
```bash
# Run this command in the helm_charts/mlflow_project folder
helm -n mlflow install lr-model . &
```
# Data preparation in dbt
To prepare a dataset for training a model, we use dbt to build tables:
- In the `source1`  and `source2` schemas (fake external sources)
- Other tables which uses data from those sources (used for training)

To prepare it, we run the command (build only tables with tags `source1` or `source2`):
```bash
dbt run -s tag:source1 tag:source2
```
## Data reproducibility
We make sure, that when we prepare a dataset for training a model within a MLflow project, we always get exactly the same dataset, no matter when we run that project.

To ensure that, we:
- Select data within a specific time frame
- Use Iceberg time travel and tags to select a snapshot of a dataset used for training
- For dimension tables that change over time (like user status), use dbt snapshots
	- Select records where `valid_from` < `date_of_training` < `valid_to`
- MLflow save logs about:
	- SQL query used to generate the data, which includes:
		- Table names
		- Iceberg version or timestamp of tables
	- Commit hash of the code used (in case someone changes the code):
		- dbt code
		- Infrastructure configuration (K8s YAML manifests used):
			- Spark
			- dbt
	- hyperparameters
# MLflow projects code
MLflow projects code - [[Data and ML platform project - MLflow projects code]].
# MLflow workflow
## Experiments
- Each experiment corresponds to a specific goal, like predicting a revenue.
- Each run in an experiment is either building a model or evaluating it
- There can be different kinds of models taking different inputs in a single experiment
## MLflow projects
- Each MLflow project contains code for building and evaluating one specific kind of model, taking specific features as an input
- Models logged by each project needs to contain information about from which project they come from (so we can evaluate only them)
- Evaluating script evaluates models from this project. Models from different projects will require different evaluation techniques as they can take different features as an input.
- Evaluating script can evaluate:
	- All the models after a specified date
	- All models
	- The latest model
	- Models with specific parameters, tags, names
## Runs
- Evaluating runs - Each run for evaluating a model, evaluates only one model and logs:
	- metrics
	- URI of the evaluated model
	- ID of the run where the evaluated model has been built
## Promoting a model (saving in a registry)
To promote a model, i.e. save it in a MLflow registry, we use the `promote_model.py` script which finds URI of the model with the best performance.

This script finds the model with the best performance by searching through runs which were:
- Evaluating models
- Saving evaluation metrics and URIs of evaluated models
and picks a URI of the model with the best metrics.