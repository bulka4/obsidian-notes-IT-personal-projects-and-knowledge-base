Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
CeleryExecutor runs Airflow tasks on a pool of long-running worker processes, coordinated through a message broker.

CeleryExecutor is a cluster of servers and worker processes can run on different servers.

Airflow scheduler talks to a message broker and broker sends tasks to do to workers.

Message broker:
- Prepared a queue for tasks
- Enables retries

Celery workers execute Python code from the task.