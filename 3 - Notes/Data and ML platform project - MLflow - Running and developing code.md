Tags: [[_My_projects]]
#MyProjects 

# Create a development pod
We can use development pods (more info here - [[Data and ML platform project - Code development & testing scripts|link]]) to develop and test MLflow code:
  ```bash
	# Run this from the helm_charts/development_pods/mlflow folder
	helm -n mlflow install dev-pod . &
  ```
# Mounted files
The `apps` folder from the host will be mounted to the created development pod. So we can edit code on the host and then run it from that pod.
# Get access to a bash session in the created pod
To get access to a bash session in the created pod so we can run commands we can:
- Attach VS Code to that pod like described here - [[Data and ML platform project - VS Code Kubernetes extension setup for code development|link]] 
  - Or use `exec -it dev-pod -- /bin/bash`
# Run MLflow projects
  Use files from the `/root/apps/mlflow_projects/linear_regression_revenue` folder to perform actions described below:
  - Use commands from the `run_script.bash` file:
	  - Run the command for training (we can create multiple models using different parameters `fit_intercept` and `positive`)
	  - Run the command for evaluating all the models
  - Run the `python3 promote_model.py` command to run the Python script which takes the best model (with the best metrics from the evaluation) and saves it in the MLflow registry
  - To delete an experiment / run, use the `delete_exp_run.py` script.
# Running MLflow projects using Helm chart
We can use the `helm_charts/mlflow_project` Helm chart to run MLflow projects which trains and evaluates ML models:
```bash
# Run this command in the helm_charts/mlflow_project folder
helm -n mlflow install lr-model . &
```