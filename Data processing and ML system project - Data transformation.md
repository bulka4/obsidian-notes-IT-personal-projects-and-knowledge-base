Tags: [[_My_projects]]
#MyProjects 

# Introduction
For data transformation we use dbt and Spark. There are two options for tools which we can use to run Spark:
- Spark Operator
- Thrift Server

Most probably the Thrift Server is the best option. It provides a long running Spark session we can reuse for many SQL queries.

Spark Operator is for batch jobs, it executes specified SQL queries and session is closed. Next time we want to execute new SQL queries, it creates a new session.
# Thrift Server
