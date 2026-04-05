Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
XCom is a tool allowing to share data between tasks. It stores data in Airflow metadata database and any task can write to it and read from it.
# When to use it
We use XCom when we need to pass information from one task to another but it is not a good option for storing big amounts of data (like big tables with a lot of data).
# Push to XCom
All the data which is returned by Airflow task functions is pushed to XCom (saved there), for example:
```python
from airflow.decorators import task

@task
def produce():
    return {"key": "value"}  # automatically pushed to XCom
```

Or we can also use the `xcom_push` command and the `ti` variable ([[Airflow - Task instance (the 'ti' variable)|link]]) to push data there:
```python
ti.xcom_push(key="my_key", value=123)
```
# Pull data from XCom
To pull data from XCom (read it), we can use the `xcom_pull` function and the `ti` variable ([[Airflow - Task instance (the 'ti' variable)|link]]):
```python
@task
def consume(ti=None):
    data = ti.xcom_pull(task_ids="produce")
    print(data)
```
# How XCom stores data
XCom stores data as key-value pairs. Default key for returned values is `return_value`.

Each XCom entry is tied to a specific DAG, Task and run (task execution) so values don’t clash across runs.