Tags: [[__Data_Engineering]]

# Introduction
Example workflow then Celery executor is used:
-  Scheduler sees tasks’ schedules and based on that, at a proper time, it asks Executor to execute a task.
-  Executor puts the task in a queue (Celery queue).
-  Workers (Celery workers) sees that task in a queue and pick it up.

Example workflow then Kubernetes executor is used:
-  Scheduler sees tasks’ schedules and based on that, at a proper time, it asks Executor to execute a task.
-  Executor tells Kubernetes to start a Pod (Worker) for this task.
-  Kubernetes creates a Pod.
-  Pod runs a task.

#DataEngineering 