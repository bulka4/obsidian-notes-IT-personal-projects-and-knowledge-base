Tags: [[_Databases]]
#Databases  

# Introduction
A query planner (also called a query optimizer) is the part of a database system that decides how to execute a SQL query efficiently.

When we write SQL, we describe what data we want and query planner decides how to get this data. It decides things like:
- Whether to use an index
- In which order to execute commands (e.g. filter first, then join tables)
- Which algorithm to use for joining

It uses database metadata and statistics to determine how to execute the query efficiently.
# Query processing stages
A simplified database pipeline:
```
SQL query
    |
    v
Parser
(check syntax, tables, columns)
    |
    v
Query planner / optimizer
(choose best execution plan)
    |
    v
Executor
(run the plan)
```
# Execution plan
An output of the query planner is an execution plan which we can see.