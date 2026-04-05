Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
To move a specific version of a registered model to a specific stage, we can use:
```python
from mlflow.tracking import MlflowClient  
  
client = MlflowClient()  
  
client.transition_model_version_stage(  
	name="my_prediction_model"
	,version="model_version"
	,stage="stage_name" # e.g "Production", "Staging", "Archived"
)
```

We need to provide a version of the model for which we want to change the stage.
# Archive existing versions
When we assign a specific model's version to a stage, we can automatically move all the other versions from that stage to the `Archived` stage by using `archive_existing_versions=True`:
```python
client.transition_model_version_stage(  
	name="my_prediction_model"
	,version=3
	,stage="stage_name" # e.g "Production", "Staging", "Archived"
	,archive_existing_versions=True
)
```
