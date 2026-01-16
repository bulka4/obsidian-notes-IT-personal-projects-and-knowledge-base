Tags: [[_dbt]] [[_Spark]]
#dbt #Spark 

# Introduction
When we want to use dbt with Spark it is better to have a persistent Spark session which we use every time we run dbt code rather than creating a new session every time.

Below are described issues which we might have if we create a new Spark session every time.
# Incremental computing
dbt logic for incremental computing depends on information provided by a database engine (Spark SQL engine in that case) and that information is lost when we finish a session, and it needs to be recreated in a new session.

For example, that is information such as:
- catalog metadata
- statistics about existing tables
- partition discovery

Because of that:
- incremental detection can behave differently
- backfills are more fragile
- performance variance increases
# Running large DAGs
When dbt runs large DAGs (many SQL statements), then with a fresh Spark session there might be problems with:
- memory pressure
- skewed joins
- shuffle blowups
### 2.3 Weaker failure isolation _inside_ a dbt run

In dbt:

- one model failing ≠ whole run failing immediately
    
- retries and partial progress matter
    

With SparkApplication:

- driver failure = entire dbt run aborted
    
- no reuse of engine state for recovery
    

With a persistent engine:

- failures are localized to statements
    
- engine survives to execute remaining models
    

This matters for large production DAGs.
# Questions
- What are memory pressure, skewed joins and shuffle blowups?
- What are backfills?
- 