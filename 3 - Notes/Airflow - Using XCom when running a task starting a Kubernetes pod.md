Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
If we want to use XCom ([[Airflow - XCom - Share data between tasks|link]]) in a task which starts a new Kubernetes pod, then we can do this if we use the `KubernetesPodOperator` operator.

If we use the `do_xcom_push=True` argument:
```python
KubernetesPodOperator(
    task_id="my_pod_task",
    ...
    do_xcom_push=True,
)
```
then in the created pod we can save data in the `/airflow/xcom/return.json` file and its content will be stored in XCom.
# Using a custom code for creating pods
If we create a Kubernetes pod in a task using a custom code (the `kubernetes.client` library), then using `/airflow/xcom/return.json` file doesn't work.