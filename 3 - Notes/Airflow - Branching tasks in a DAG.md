Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
Airflow provides a [branching decorator](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/dags.html#concepts-branching) that allows to return the task_id (or list of task_ids) that should run:
```python
@task.branch(task_id="branch_task")
def branch_func(ti):
    xcom_value = int(ti.xcom_pull(task_ids="start_task"))
    if xcom_value >= 5:
        return "big_task" # run just this one task, skip all else
    elif xcom_value >= 3:
        return ["small_task", "warn_task"] # run these, skip all else
    else:
        return None # skip everything
```