Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Task dependency chaining
We can create a chain of tasks where each task runs immediately after all the previous tasks has been finished and defining that is super simple.

We can run all tasks one after another by defining:
```python
task_1 >> task_2 >> task_3
```

Or we can also run some tasks in parallel:
```python
task_1 >> [task_2, task_3] >> task_4
```
then:
- `task_2` and `task_3` runs in parallel after the `task_1` has been finished
- After both `task_2` and `task_3` has been finished successfully, the `task_4` runs
# UI
Airflow provides UI where we can monitor jobs and see a graph showing what tasks we have in a job and what are the dependencies between them.
# Scalability
Works with executors like Celery or Kubernetes, so each task can run either on a single machine or any machine in a cluster.
# Extensibility
A lot of of built-in operators (SQL, Spark, cloud services) and easy to create our own (in Python, more info here - [[Airflow - Custom operators|link]]).
# Dynamic pipelines
Generate tasks programmatically (e.g., per table/partition) using Python ([[Airflow - Dynamic tasks|link]]).
# Multi-DAG dependencies
We can create a dependencies between DAGs ([[Airflow - DAGs|link]]) like described here - [[Airflow - Multi-DAG dependencies|link]].
# XCom (inter-task communication)
Pass data between tasks without external storage ([[Airflow - XCom - Share data between tasks|link]]).
# Pools & concurrency limits
Pools ([[Airflow - Pools|link]]) allows us to limit how many tasks can use a resource in parallel. This helps to:
- Control resource usage
- Prevent overload of external systems
# Sensors
Sensor is a task which can wait for events to happen instead of being triggered at a specific time. 

The entire DAG ([[Airflow - DAGs|link]]) is still being triggered at a specific time but:
- A sensor task will wait for an event
- Once an event occurs, the sensor task succeeds and the DAG continues executing next, downstream tasks

More info about sensors is here - [[Airflow - Sensors|link]].
# Version-controlled workflows
DAGs ([[Airflow - DAGs|link]]) are just Python code, so we can manage them in Git and review changes.
# Backfills & partial reruns
We can rerun ([[Airflow - Rerunning tasks|link]]):
- single task
- subset of DAG
- historical intervals
- only failed tasks

We can use for that:
- UI
- CLI
- API
# Retries & Failure handling
## Retries and timeouts
- Exponential backoff (increase delay between retries to avoid hammering a failing system)
- Retry delay tuning (control how quickly tasks retry depending on failure type)
- Timeouts (Task fails if it doesn't finish within a specified time)
## Failure handling
- Trigger rules
    - lets us define when a task runs based on upstream results (success, failure, skipped)
    - For example we can run a task only when:
	    - All the upstream tasks succeeded
	    - At least one upstream task failed
- Fallback tasks
    - lets us define what to do when a task fails
    - e.g., run cleanup, rollback, or alternative logic
## Detailed logging & observability
- Per-task logs stored and accessible in UI
- Helps debug failures without extra tooling
## Executor-level fault tolerance
With executors like Celery or Kubernetes:
- tasks can be retried on different workers ([[Airflow - Worker|link]]) (processes executing tasks) or nodes (servers)
- worker crashes don’t kill the whole pipeline
## Callbacks
We can attach to tasks Python functions that run on events:
- `on_failure_callback` → run code when task fails
- `on_retry_callback` → run code on each retry
- `on_success_callback` → run code when task succeeds

Example use:
- send Slack message on failure
- log custom metrics
- trigger cleanup job
### Context-aware callbacks
Callbacks can receive task context:
- task instance info
- execution date
- logs / metadata

So we can build dynamic alerts about DAGs ([[Airflow - DAGs|link]]) like:
> “Table X failed in DAG Y for run date Z”
# Alerting
## Alerts
- Built-in email alerts
- Easy integration with Slack, etc.
## DAG-level callbacks and alerts
- Set up callbacks and alerts at a DAG ([[Airflow - DAGs|link]]) level instead of per-task.
- Useful for global alerts like “pipeline broken”.
# Monitoring
## SLA monitoring
We can configure a DAG to trigger an SLA miss if a task doesn't finish within a specified time frame. The task continues, it only sends an alert and it is not marked as failed.

Airflow doesn't just sent an alert about an SLA miss but it can also trigger custom workflows.
## Metrics for monitoring
Airflow can emit runtime metrics automatically, not just logs:
- task duration
- DAG duration
- success/failure counts
- scheduler lag
- queue wait times

This can be used for dashboards + alerting systems (like Prometheus and Grafana)
## Scheduler & system health monitoring
Beyond tasks, Airflow monitors itself:
- scheduler heartbeat failures
- DAG parsing delays
- queue backlog growth
- worker ([[Airflow - Worker|link]]) availability

Useful for detecting Airflow infrastructure issues, not pipeline issues.
## Pool & queue monitoring alerts
Airflow can notify us when:
- pool ([[Airflow - Pools|link]]) is saturated (no free slots)
- tasks are stuck in queue too long
- queue backlog is growing
- workers ([[Airflow - Worker|link]]) are not consuming tasks fast enough

Here queue refers to both waiting for a worker process and a pool slot.

Helps detect bottlenecks before failures happen
## External task monitoring (ExternalTaskSensor + deferrable tracking)
When one DAG depends on another DAG, then Airflow can alert about a DAG having a dependency DAG failed.

For example, if a DAG A depends on a DAG B and DAG B fails, then Airflow will alert that the DAG A has a failed dependency.