Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
We can define a dependency between DAGs ([[Airflow - DAGs|link]]) to define that DAG B should run (or continue) only after DAG A reaches a certain state.
# How it’s implemented
## 1. ExternalTaskSensor (classic way)
DAG B waits for:
- a specific task in DAG A
- or the whole DAG A

Example idea:
- “Wait until `extract_dag` finishes successfully before starting transform”
## 2. Dataset-based dependencies (modern way)
Airflow supports **datasets**:
- DAG A produces a dataset
- DAG B is triggered when that dataset is updated

more decoupled, event-driven
# Why use multi-DAG dependencies
- Split large pipelines into smaller DAGs
- Separate responsibilities (ingestion, transformation, ML, etc.)
- Reuse upstream pipelines across multiple downstream DAGs