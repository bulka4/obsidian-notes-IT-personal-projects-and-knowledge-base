Tags: [[__Data_Engineering]]
#DataEngineering 

# What “dependencies” mean in data pipelines
In data pipelines we have dependencies like:
- Ingest data before transforming it
- Clean data before aggregating it
- Build tables before running analytics or ML models

So dependencies define:
- Execution order (A → B → C)
- Conditions (run B only if A succeeds)
- Data readiness (run only when data is available)
# Types of dependencies
### 1. Task dependencies (control flow)
The most basic type:
- Task B runs only after Task A completes

Example:
- Extract → Transform → Load

Tools like Apache Airflow model this as a DAG (Directed Acyclic Graph).
### 2. Data dependencies
A task depends on data availability, not just another task.

Example:
- Wait until a partition arrives in a data lake before processing

Common in:
- Apache Spark jobs
- Event-driven pipelines
### 3. Time-based dependencies
Tasks run on schedules, e.g. daily at 2 AM.

But often combined with data checks (e.g., “run at 2 AM **if data is ready**”).
### 4. External dependencies
Dependencies on:
- APIs
- Databases
- External systems

Example:
- Wait for a file in S3 or a table update in a warehouse
### 5. Conditional dependencies
Execution depends on logic:
- If data quality passes → continue
- Else → stop or trigger alert
## 6. Cross-system pipeline dependencies
There are two problems:
- When upstream task runs, all the downstream tasks must run as well
- Downstream tasks can't run if the upstream tasks didn't finish yet

This is a problem when those tasks are in different pipelines / DAGs.

Solutions:
- External dependency tracking
- Event-based scheduling
- Data-aware orchestration
# Dependency management strategies
## 1. Explicit task chaining
Define dependencies manually.
- Simple  
- Hard to scale in large pipelines
## 2. Event-based scheduling
Trigger tasks based on events, not just time, for example:
- file in S3
- table update in a warehouse

Example:
- Dagster asset-based model
- Apache Airflow datasets feature, sensors
## 3. Data-aware orchestration
Tools like Dagster:
- Track **data lineage explicitly**
- Know:
    - “Dataset B depends on Dataset A”

So when A is recomputed:  
- B is automatically marked “stale” and recomputed

Or in Airflow the dataset features can trigger a pipeline once a specific dataset has been updated by another pipeline.

We can define which dataset is being updated by a pipeline and which dataset needs to be updated in order to trigger a pipeline
## 4. External dependency tracking
We might be able to check a task's status from another pipeline. 

For example in Apache Airflow, we can use `ExternalTaskSensor` so that Pipeline B waits for Pipeline A’s output.
## 5. Idempotency
Tasks should be safe to rerun if it fails due to a failed dependency:
- Avoid duplicate outputs
- Ensure deterministic results

This reduces dependency fragility.
## 6. Dependency isolation
Instead of:
- Relying on internal states of upstream jobs

Use:
- Stable interfaces (tables, files, APIs)

By internal states we mean things like:
- job logic
- logs
- temporary tables / files
- partial or staging data

If an upstream job relies on such internal states of a downstream job, there might be issues like:
- Temporary file got changed name, location, or format, or it got deleted
- Logic has changed (but the final output is the same)
- Logs message has changed slightly

So relying on them is fragile.

Stable interfaces we should rely on, are for example:
- Final output table / file
- API endpoints returning a specific data
- Events, metadata - e.g. - Event: `data_ready = true` or a dataset update in Apache Airflow
## 7. Time + validation hybrid
Very common pattern:
- Run at scheduled time
- Validate external dependency

Example:
- Run at 2 AM
- But only proceed if data exists
## 8. Data lineage
More info here - [[Data Engineering - Data lineage|link]].

Track dependencies across: Tables, Pipelines, Transformations. 

Tools: 
- OpenLineage
## 9. Decoupling via storage
Instead of:
- Pipeline A triggering another pipeline B or sending data to it directly

Use:
- Pipeline A writes data and pipeline B reads it later
- Both pipelines are triggered separately (e.g. by a schedule or an event)

Thanks to this:
- B doesn't depend on A being alive and available
- Easier to change A without breaking B
- No tight timing dependencies
- Independent deployment of pipelines
- Easier retries/backfills
- Better scalability
## 10. Contract-based data pipelines
Data pipelines can use a contract which describes how data should look like so those pipelines work correctly.

Thanks to that, pipelines depend on agreed data rules instead of implementation details of those pipelines.

More info here - [[Data Engineering - Contract-based data pipelines]]

Contract describes:
- Schema (column names, data types etc.)
- Data quality (no nulls, values in valid ranged etc.)
# Practices
## Caching results
When we need to rerun a job with multiple tasks and for one task, inputs which it depends on didn't change, we can skip this task and use its previous output.
## Retries with backoff
Instead of:
- Retry immediately

Use:
- Retry after 1s → 2s → 4s → 8s
## Circuit breakers
- A protection mechanism for handling unreliable external dependencies (like APIs).
- Used for example when we try to make an API call many times, regularly.
- Prevents from performing too many failing actions.

More info here - [[Software Engineering - Circuit breakers]].
## Timeouts
Never wait forever:
- Fail fast if dependency isn’t ready
# Common failure scenarios
### 1. Data arrives late
- Problem: Pipeline runs but fails due to missing data
- Solution: data-aware scheduling
### 2. API partially fails
- Problem: You ingest incomplete data
- Solution: validation + retries
### 3. Schema changes silently
- Problem: Pipeline breaks downstream
- Solution: schema contracts
### 4. External system outage
- Problem: Entire pipeline blocked
- Solution: fallback + alerting