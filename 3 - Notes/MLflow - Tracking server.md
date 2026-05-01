Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
MLflow tracking server is a HTTP server used for experiment tracking ([[MLflow - Experiment tracking|link]]), i.e. to save metadata and artifacts.

When we run a MLflow script, it communicates with a tracking server to save or read data. We use for that MLflow client API (`mlflow.log_param()`, `mlflow.log_metric()`, etc.).
# UI
MLflow tracking server also provides a UI where we can review experiments and runs ([[MLflow - Experiments and runs|link]]) with saved metadata or model registry ([[MLflow - Registry|link]]).
# Backend store
Backend store is used by a tracking server to store metadata, like:
- Experiment info
- Run UUIDs
- Parameters
- Metrics
- Tags
- Run start/stop times

It is usually a SQL DB like MySQL, Postgres, or SQLite.
# Artifact store
Artifact store is used to store artifacts (files), like:
- Saved models
- Plots
- Logs

For example, it can be Azure Blob Storage, AWS S3, local FS
# Starting a tracking server
We start a Tracking Server with a single command:
```bash
mlflow server \
	--host 0.0.0.0 \
	--port 8885 \
	--backend-store-uri <url> \
	--artifacts-destination <url>
```
