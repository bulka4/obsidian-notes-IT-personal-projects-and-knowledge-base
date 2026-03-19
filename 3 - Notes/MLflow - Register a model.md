Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Register a model
Register a model ([[MLflow - Registry|link]]):
```python
import mlflow

model_uri = f"runs:/{run_id}/model"

mlflow.register_model(model_uri, "my_prediction_model")
```
# Promote a version to production
Promote a model version to production:
```python
from mlflow.tracking import MlflowClient  
  
client = MlflowClient()  
  
client.transition_model_version_stage(  
	name="my_prediction_model",  
	version=3,  
	stage="Production"  
)
```
# Load registered model
Load registered model:
```python
import mlflow.pyfunc  
  
model = mlflow.pyfunc.load_model("models:/my_prediction_model/Production")
```
