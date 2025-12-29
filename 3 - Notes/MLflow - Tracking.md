Tags: [[__Machine_Learning_Engineering]]

# Introduction
## MLflow Tracking
Tracking is a centralized experiment logger where you track:
- **Parameters:** Hyperparameters like learning rate, batch size, etc.
- **Metrics:** Accuracy, loss, AUC, any numeric measure
- **Artifacts:** Model files, plots, datasets, any output file
- **Source info:** Git commit hashes, code version, who ran it, when

You log these from your training scripts with the MLflow client API (mlflow.log_param(), mlflow.log_metric(), etc.).

You can then visualize and compare experiments in the MLflow UI.

For tracking we are using 3 components:
- A **backend store**
- An **artifact store**
- MLflow Server (**Tracking Server**)
### A backend store
- usually a SQL DB like MySQL, Postgres, or SQLite
- Stores metadata:
	- Experiment info
	- Run UUIDs
	- Parameters
	- Metrics
	- Tags
	- Run start/stop times
### An artifact store
- For example Azure Blob Storage, AWS S3, local FS
- Stores files:
	- Saved models
	- Plots
	- Logs
### MLflow Server (Tracking Server)
- Provides UI
- Clients (your scripts or projects) send data here
- It orchestrates:
	- Logging to the **backend store**
	- Uploading to the **artifact store**
	- Serving the **web UI** to browse runs

We set up a Tracking Server with a single command:
![[2 - Images/MLflow/Screenshot 1.png]]


#MLEngineering 