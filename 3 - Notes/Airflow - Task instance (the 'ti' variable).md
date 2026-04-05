Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
In Airflow task we have an access to the `ti` variable which represents a specific run of a specific task.

Every time we run a task, Airflow creates this variable representing this task run.

`ti` gives us an access to a runtime context, including:
- `XCom` push/pull ([[Airflow - XCom - Share data between tasks|link]])
- task metadata
- execution info

This variable is available only in Airflow tasks:
```python
@task
def my_task(ti=None):
    ti.xcom_push(...)
```
We need to pass the `ti=None` argument so we can use the `ti` variable inside the task function.
# Task starting a new Kubernetes pod
If our task creates a new Kubernetes pod and runs code there, then inside that pod there is no access to the `ti` variable. Only in the task function which starts that pod we can access it.