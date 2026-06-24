Tags: [[__MLOps]]
#MLOps 

# Introduction
In ML, CI is an automatic verification that changes don’t break our ML system.

Those “changes” can be:
- code (training scripts, feature engineering)
- configs (hyperparameters)
- sometimes even data schemas

The key idea:
> Every change should be tested and validated automatically before training or deployment
# What happens in ML CI
## 1. Trigger
CI starts when:
- There is a change in the code for creating the model (e.g. in the code preparing training data or training the model)
- Monitoring systems detects that model's performance drops and it should be replaced by a new model

Example:
>You modify a feature engineering function → CI runs automatically
## 2. Code validation (classic software CI)
Prepare unit and integration tests ([[Software Engineering - Unit and integration tests|link]]) to test on a small sample of data:
- Training ML models (check if model does train (loss drops))
- Does Airflow DAGs run successfully (e.g. for data processing and training ML models)
- Whether MLflow logs metrics and models successfully

Additionally check:
- linting (flake8, black) ([[Software Engineering - Linting|link]])
## 3. Data validation (ML-specific)
Check if data is correct after updating the code. More info - [[Data Engineering - Data validation]].
## 4. Train a model
Train a new model(s).
## 5. Evaluate and save the best model
Evaluate all the trained new models and save the best one.