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
CI starts when something changes:
- Git push
- Pull request
- Config update

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
