Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
MLflow project helps to package our ML code with all dependencies to make it reproducible and shareable.

That can include code for:
- Training models
- Preprocess data
- Run evaluations

MLflow project is a folder containing:
- MLflow project file ([[MLflow - Projects - MLproject file|link]])
- Scripts (e.g. `preprocess.py`, `train.py`, `evaluate.py`)
- Files for environment setup (e.g. `conda.yaml`, `Dockerfile`)
- Any other files
# MLproject file
A MLproject file is a YAML file which describes the project. More info can be found here - [[MLflow - Projects - MLproject file]].
# Entry points
An entry point is a parametrized command to run a Python script, e.g. for training a model.

More info can be found here - [[MLflow - Projects - Entrypoint]].
# Environment preparation
In a MLflow project, we can specify how to prepare an environment for running entrypoints. We can use for that:
- Conda
- Docker

More info is here - [[MLflow - Projects - Environment preparation]].