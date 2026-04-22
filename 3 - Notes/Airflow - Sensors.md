Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
A sensor is a special type of Airflow task that waits for a certain condition to be true, for some event to occur before allowing the DAG to continue executing downstream tasks.

A sensor can wait for an external event, like a file arriving in storage, a new database row or a new database row with a specific value.
# DAG workflow with a sensor task
The workflow is like that:
- DAG is triggered at a specific time
- Once a sensor task is reached (it starts execution), it waits for an event to occur
- Once an event occurs, the sensor task succeeds and the DAG continues with next, downstream tasks

It is not like a sensor task will run all the time, execute some function every time an event happens and then again wait for the next event. 
# How sensors detect events
A sensor doesn't receive push events, that is it can't be triggered by other process sending data to it.

Instead, a sensor:
- Polls repeatedly (checks condition every X seconds)
- Evaluate a condition (file exists, query returns result, etc.)
- When condition is true → task succeeds → DAG continues
# Example sensors
## 1. File exists sensor
Waits for a file to appear (e.g., in S3, HDFS, local FS)
```python
FileSensor(  
    task_id="wait_for_file",  
    filepath="/data/input.csv",  
)
```
## 2. S3 / cloud object sensor
Wait for a file in cloud storage
```python
S3KeySensor(  
    task_id="wait_for_s3",  
    bucket_name="my-bucket",  
    bucket_key="data/file.csv",  
)
```
## 3. Database sensor
Wait for a row or condition in DB
```python
SqlSensor(  
    task_id="wait_for_data",  
    conn_id="postgres_db",  
    sql="SELECT 1 FROM orders WHERE processed = true",  
)
```
## 4. HTTP sensor
Wait for an API response to return success
```python
HttpSensor(  
    task_id="wait_for_api",  
    http_conn_id="my_api",  
    endpoint="status/job/123",  
)
```
# Creating a custom sensor
We can create a custom sensor like this:
```python
from airflow.sensors.base import BaseSensorOperator

class MySensor(BaseSensorOperator):
    def poke(self, context):
        return check_condition()
```
- We use the `BaseSensorOperator` as a parent class, not `BaseOperator` like in a normal custom operator ([[Airflow - Custom operators|link]])
- We need to define the `poke` function which checks a condition and returns True or False
# Event-driven triggers
A similar concept are event-driven triggers, more info about them is here - [[Airflow - Event-driven triggers]].