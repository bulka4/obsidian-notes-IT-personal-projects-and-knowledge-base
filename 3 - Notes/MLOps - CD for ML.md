Tags: [[__MLOps]]
#MLOps 

# Introduction
Below is described step-by-step CD flow for ML.
## 1. Model is trained and saved
- Model is trained in a pipeline (e.g. using Airflow)
- Saved and versioned (we save a new model as a new version of the existing one) (e.g. in MLflow)
## 2. Model evaluation
Before deployment:
- compare with current production model
- check metrics (accuracy, F1, etc.)

Example:
```
if new_model.f1 > production_model.f1:  
    proceed  
else:  
    reject
```
## 3. Promotion (staging → production)
We move model to a location from where it will be loaded in a production pipeline for making predictions.

For example, in MLflow we move model to a proper stage in registry (from stage to prod) or assign a proper alias (prod).
## 4. Deployment (actual CD)
If we don't have deployed code which uses created ML model, then in this step we deploy it. 

Otherwise, we only promote a model what was done in the previous step, i.e. we save a model in a location from where it will be used by an already deployed code.

If we need to deploy code additionally, then we deploy for example:
- Online serving (API)
	- deploy model as REST API
	- e.g. FastAPI on Kubernetes
- Batch scoring
	- scheduled predictions in Airflow
## 5. Release strategies (advanced CD)
Instead of just replacing the old model, we can use:
- **Canary deployment** → small % of traffic ([[MLOps - Canary & shadow deployment|link]])
- **A/B testing** → compare models live ([[MLOps - A-B testing|link]])
- **Shadow deployment** → run silently ([[MLOps - Canary & shadow deployment|link]])
## 6. Monitoring (part of CD loop)
After deployment monitor:
- data drift
- prediction distribution
- performance metrics

If something breaks -> rollback.

More info about monitoring can be found here - [[MLOps - Monitoring]].
# Questions
- 