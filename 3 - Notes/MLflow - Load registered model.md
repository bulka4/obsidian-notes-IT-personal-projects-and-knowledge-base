Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
To load registered model we can use:
```python
import mlflow.pyfunc  
  
model = mlflow.pyfunc.load_model(model_uri)
```
as `model_uri` we can use:
- `models:/model_name/stage_name`
- `models:/model_name/version`