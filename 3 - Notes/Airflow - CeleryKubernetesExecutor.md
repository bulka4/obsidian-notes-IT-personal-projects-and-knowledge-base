Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
With CeleryKubernetesExecutor, we have two task execution types:
- Default tasks are executed by Celery workers ([[Airflow - CeleryExecutor|link]])
- Kubernetes tasks runs in their own Kubernetes pods (like in KubernetesExecutor - [[Airflow - KubernetesExecutor|link]])

