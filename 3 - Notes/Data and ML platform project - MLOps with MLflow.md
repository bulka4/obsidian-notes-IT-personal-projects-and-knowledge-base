Tags: [[_My_projects]]
#MyProjects 

# Questions
- What is canary testing or shadow deployment
	- can be used for retrained models before moving them into prod
- what are unit tests for dbt models and integration tests for ML pipelines
# MLflow
Notes about how do we use MLflow for creating and evaluating models are here - [[Data and ML platform project - MLOps - MLflow workflow]].

Notes about MLflow code - [[Data and ML platform project - Code - MLflow projects]].

Notes about how we can develop MLflow code - [[Data and ML platform project - Code development & testing scripts]].
# ML model creation
## Data preparation
To prepare a dataset for a model, it is probably better to prepare it together with other datasets within the same dbt run, outside of a MLflow project.

Preparing a dataset within a MLflow project might make sense only if we know, that this dataset will be used only for this one model and nothing else.
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
## Model storage
Maintain a model registry with stages (Staging, Production, Archived).
# Making and saving predictions
How do we make and save predictions is explained here - [[Data and ML platform project - Making and saving predictions]]
# ML model performance monitoring
We monitor ML model performance over time as new data arrives. 

We save ML models predictions in tables as described in the previous section. We use those predictions to:
- Perform calculations described below to calculate metrics 
- Save those metrics in tables
- Use saved metrics to decide whether or not a model needs retraining.

We perform those calculations using dbt whenever possible and Python for more complex calculations, and save results in tables.
## Metrics for monitoring
This section described metrics we calculate and save in table which will be then used to decide whether or not a model needs retraining.
### Model performance
Using predictions saved in tables, dbt can calculate metrics like:
- Accuracy, RMSE etc
### Prediction behavior
Check:
- Prediction mean
- Prediction variance
- Class balance
- Confidence distribution
- feature importance drift monitoring
- SHAP value drift

If those values changes significantly, something might be wrong.

We can calculate some of those values using dbt, and more complicated ones using Python. Results will be saved in a separate table from where can be used for monitoring.
### Data drift
Check for new data:
- Feature distributions
- Null rates
- Cardinality
- Summary stats
- KL divergence
- Wasserstein distance

and compare it with the data used for training. If those values are different, then model can start making bad predictions.

This way we can detect problems with predictions before they appear.
## Prometheus / Grafana for monitoring
Use Prometheus / Grafana for monitoring those metrics.
# Updating models
We run a long running Python script which observes metrics described in the previous section (model performance, prediction behavior, data drift) and when specific conditions are satisfied (when model performs badly), it creates a new model and replaces the old one with it.

It works like that:
- Checks values of metrics described in the previous section (model performance, prediction behavior, data drift)
- Based on the metrics decides whether or not the model requires retraining (we check if the model performs badly or may start to do so)
- if specified conditions are satisfied, it runs a MLflow projects in a Kubernetes pod using Kubernetes Python client which prepare new models
	- We use for that Airflow conditional tasks
	- Each new trained model with metrics about their performance is saved in MLflow
- Updates the model used in production
	- Checks models' performance from MLflow database
	- Picks up the best model
	- Saves the model in a specified location which will be used in a production pipeline