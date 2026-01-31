Tags: [[_dbt]] [[_Spark]]
#dbt #Spark 

# Introduction
When using dbt with Spark, it is generally better to use a persistent Spark session ([[Spark - Session|link]]) (for example via Spark Thrift Server) rather than creating a new Spark session for every dbt run.

This recommendation applies specifically to dbt-style workloads, which execute many SQL statements which uses database metadata a lot and expect database-like behavior.

Below are the main issues that can arise when a new Spark session is created for every dbt run.
# Loading metadata
For every new Spark session, Spark must reload metadata from the catalog (table schemas, file locations, partitions, statistics).

This takes additional time and is especially relevant for dbt ([[dbt - Using a catalog|link]]), which:
- frequently inspects metadata
- relies on catalog information for features like incremental models

With a persistent session, this metadata stays cached and up to date.
# Execution plans
For each SQL statement, Spark creates an execution plan, which determines how the query is executed (for example join strategies, data shuffling, memory usage).

Spark always generates a new execution plan for each query, but:
- a fresh session has less metadata and runtime context
- a long-lived session has cached metadata and statistics

As a result:
- the final query result is the same
- but the execution strategy and performance can differ between sessions
# Loss of runtime optimizations
During its lifetime, a Spark session accumulates useful runtime information which can be used for optimization, such as:
- cached metadata
- table and column statistics (row count etc)
- cached datasets (`CACHE TABLE`)
- adaptive query execution feedback
- warm JVM and code generation

When a new session is created, all of this information is lost and must be rebuilt.
# Harder failure recovery
If a dbt run fails:
- with a persistent session, only the failed queries need to be rerun
- with a new Spark session, the entire environment must be recreated (metadata loading, creating execution plans etc)

This makes retries slower and more expensive.
# Harder debugging
With a persistent session, we can:
- Inspect session
- Run new queries for testing
- examine loaded metadata and cached data

With short-lived Spark applications, debugging is limited to logs after the session has already terminated.
# Configuration and environment consistency (important)
Each new Spark session must reapply:
- Spark configuration
- extensions (Iceberg, Delta, Hive)
- catalog settings

This increases the risk of configuration drift and makes it harder to guarantee consistent behavior across dbt runs.
# Questions
- 