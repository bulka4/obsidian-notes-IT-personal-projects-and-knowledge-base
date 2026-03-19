Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Accessing services UIs
We can access UIs of different services by using below URLs in a browser:
- Airflow UI - `localhost:8080`
- MLflow Tracking server UI - `localhost:5000`
# Running SQL queries with Beeline CLI tool
To test data we created in a Spark catalog, we can:
- Connect to the pod running Spark Thrift server:
  ```bash
  kubectl -n spark exec -it <pod-name> -- /bin/bash
  ```
- Connect to Spark using Beeline:
    ```bash
    /opt/spark/bin/beeline -u jdbc:hive2://localhost:10000
    ```
- Then, we can run SQL queries
# Example workflow
This section describes how we can manually perform different tasks using this platform:
- Data transformation
- Training and saving ML models
- Making predictions and saving them

How to perform those tasks manually is described in sections below. All those tasks can be also orchestrated with Airflow as described here - [[Data and ML platform project - Workflow orchestration with Airflow]].
## Data transformation
Run dbt model to build tables:
  ```bash
	# Connect to the dbt pod
	kubectl -n spark exec -it dbt -- /bin/bash
	# Run dbt model inside the dbt pod
	dbt run
  ```
  That should create tables visible in Azure Data Lake
## Train and save ML models
Train models using MLflow:
- Deploy a pod for code development:
  ```bash
	# Run this from the helm_charts/development_pod/mlflow folder
	helm -n mlflow install dev-pod . &
  ```
  - Attach VS Code to that pod like described here - [[Data and ML platform project - VS Code Kubernetes extension setup for code development|link]] 
  - Use files from the `mlflow_projects/linear_regression_revenue` folder to perform actions described below
  - From VS Code, use commands from the `run_script.bash` file:
	  - Run the command for training (we can create multiple models using different parameters `fit_intercept` and `positive`)
	  - Run the command for evaluating all the models
  - Run the `python3 promote_model.py` command to run the Python script which takes the best model (with the best metrics from the evaluation) and saves it in the MLflow registry
## Make and save predictions
For making and saving predictions we can use two scripts:
- `/apps/test/make_predictions_spark_operator.py` - to be run with Spark Operator
- `/apps/test/make_predictions.py` - to be run without Spark Operator, using Python

How they work is described here - [[Data and ML platform project - Making and saving predictions]].

How to run those scripts is described in sections below.
### Spark Operator
In order to run the `/apps/test/make_predictions_spark_operator.py` script using Spark Operator, we need to perform the steps below (we can perform them from the Docker image for interacting with Kubernetes - [[Data and ML platform project - Docker image for interacting with Kubernetes|link]]):
- Install Spark Operator (use commands from the `helm_scripts/install_spark_operator.sh` script)
- Install the Helm chart:
```bash
# Run this command from the helm_charts/spark_operator folder
helm -n spark install predict . &
```

This will create Spark driver and executor pods and run the Spark app `make_predictions_spark_operator.py`.
### Python
In order to run the `/apps/test/make_predictions.py` script using Python, we can:
- Create a development pod using the `helm_charts/development_pods/mlflow` Helm chart
- Attach VS Code to the created pod or use `exec -it` to get access to pod's shell
- Run the `python3 make_predictions.py` command

More about development pods and attaching VS Code can be found here - [[Data and ML platform project - Code development & testing scripts]]