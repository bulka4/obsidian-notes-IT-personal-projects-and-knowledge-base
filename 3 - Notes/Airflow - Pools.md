Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
In Apache Airflow, pools are a built-in way to limit concurrency for specific resources, how many processes can use one resource at a time.

A pool is:
> a named group with a fixed number of slots.

And a slot:
> is used by tasks to access specific resources.

Each task assigned to a pool:
- consumes 1 (or more) slots while running
- must wait if no slots are available
# Why pools exist
They protect external systems or expensive resources, for example:
- databases (avoid too many concurrent queries)
- APIs (respect rate limits)
- Spark clusters (limit parallel jobs)
- legacy systems (handle only a few jobs at once)
# Common resources that pools limit access to
## 1. External systems
- Databases (Postgres, Snowflake, etc.)
- APIs (rate-limited services)
- Data warehouses

e.g. “max 5 concurrent queries”
## 2. Compute systems
- Apache Spark jobs
- batch processing clusters
- GPU jobs

e.g. “only 2 Spark jobs at once”
## 3. Infrastructure limits
- limited network bandwidth
- shared file systems
- legacy services that can’t handle load
## 4. Cost-controlled resources
- expensive jobs (e.g. cloud processing)
- third-party paid APIs

e.g. “don’t run more than 3 at a time to control cost”