Tags: [[__Machine_Learning_Engineering]]

# Introduction
When we load a model, we can identify it using run ID and model name:
- mlflow.sklearn.load_model(f"runs:/{run_id}/model_name")

In order to get run ID we can query all the runs as described in the next ‘Querying runs’ section in this document.

#MLEngineering 