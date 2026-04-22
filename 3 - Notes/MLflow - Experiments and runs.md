Tags: [[__Machine_Learning_Engineering]]

# Introduction
A run represents a single run of a MLflow code (for building a model, evaluating it, preparing data, anything).

An experiment is a group of runs. It is a way to organize runs.

Every time we run a MLflow code:
- We choose to which experiment it should belong 
- It gets assigned automatically a run ID
- Run IDs are unique across all experiments

#MLEngineering 