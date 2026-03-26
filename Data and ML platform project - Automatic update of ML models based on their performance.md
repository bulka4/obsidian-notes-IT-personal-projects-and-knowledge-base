Tags: [[_My_projects]]
#MyProjects 

# Introduction
We run a long running Python script which observes metrics described in the previous section (model performance, prediction behavior, data drift) and when specific conditions are satisfied (when model performs badly), it creates a new model and replaces the old one with it.

It works like that:
- Checks values of metrics saved in an Iceberg table (model performance, prediction behavior, data drift)
- Based on the metrics decides whether or not the model requires retraining (we check if the model performs badly or may start to do so)
- if specified conditions are satisfied, it runs a MLflow projects in a Kubernetes pod using Kubernetes Python client which prepare new models
	- We use for that Airflow conditional tasks
	- Each new trained model with metrics about their performance is saved in MLflow
- Updates the model used in production
	- Checks models' performance from MLflow database
	- Picks up the best model
	- Saves the model in a specified location which will be used in a production pipeline