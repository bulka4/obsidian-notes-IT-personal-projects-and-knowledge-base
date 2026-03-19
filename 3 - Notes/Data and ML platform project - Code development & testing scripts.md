Tags: [[_My_projects]]
#MyProjects 

# Introduction
For developing code we can create a development pod and connect to it so we can run code inside of it and modify files.
# Development pods
In the `helm_charts/development_pods` folder we have Helm charts which can be used for code development and testing. Using them, we can:
- Create a pod with prepared environment
- Start interactive shell session using `exec -it` or attach VS Code to the created pod so we can run shell commands in it to run our code

Available development pods in the `development_pods` folder are:
- `mlflow` - Contains everything to run MLflow and Spark
# Attaching VS Code to a pod
How to use VS Code Kubernetes extension, to attach VS Code to a pod as described here - [[Data and ML platform project - VS Code Kubernetes extension setup for code development]].
# Scripts for testing
Below are described scripts we can use for testing different functionalities.
## MLflow
Scripts for testing code:
- `apps/test/make_predictions.py` - Make predictions using MLflow and save predictions in the Iceberg catalog using Spark (not Thrift server but create a new Spark driver)
## Spark
Scripts for testing code:
- `/apps/test/spark_save_data.py` - Saving data using Spark running in the client mode (Spark driver runs on the same server where we run this script).
- Scripts for making and saving predictions (more info about it is here - [[Data and ML platform project - Making and saving predictions|link]]):
	- `/apps/test/make_predictions_spark_operator.py` - Script to run using Spark Operator
	- `/apps/test/make_predictions.py` - Script to run without Spark Operator (we can run it with Python)
- 