Tags: [[_My_projects]]
#MyProjects 

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
# MLflow tags
Tags we use in MLflow projects:
- `created_model_uri` - URI of the model created in the given run
- `evaluated_model_uri` - URI of the model only evaluated in the given run (but created in another run)
- `evaluated_model_source_run_id` - Run ID where the model which has been evaluated, was created
# MLflow project parameters
When running MLflow projects, we provide parameters such as:
- Start and end date - A date range for which to select data used for training or evaluation
- Model hyperparameters - To use for training
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