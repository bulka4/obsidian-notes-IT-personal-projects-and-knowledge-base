Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
It decides how / where to run tasks from DAGs. It prepares a task to be executed by a Worker. What executor is doing exactly depends on what executor we are using.

For example about how it works please refer to the ‘Example workflow – Scheduler, Executor and Worker‘ section of this documentation.
# Kubernetes executors
When we run Airflow on Kubernetes, available executors include:
- KubernetesExecutor - [[Airflow - KubernetesExecutor|link]]
- CeleryKubernetesExecutor - [[Airflow - CeleryKubernetesExecutor|link]]
# Other executors
Executors available outside of Kubernetes include:
- CeleryExecutor - [[Airflow - CeleryExecutor|link]]