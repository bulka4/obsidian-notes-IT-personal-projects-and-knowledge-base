Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
To register a model ([[MLflow - Registry|link]]) we can use:
```python
import mlflow

model_uri = f"runs:/{run_id}/model"

model = mlflow.register_model(model_uri, "my_prediction_model")
```

The returned `model` variable contains info about the registered model. It has attributes such as:
- `version` - Version of the registered model

# Load registered model
