Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document is a part of the documentation for Data and ML platform project - [[Data and ML platform project]].

For using dbt with Airflow we have few options:
- Run the entire dbt project in one pod created by Airflow pod operator
- Split dbt project into multiple parts and run each of them in a separate pod created by Airflow pod operator (specify in pods which parts dbt should run). For example each part can consists of models with a specific tag and we can build only those models with one command.
- Use cosmos so each model becomes a separate Airflow task and runs in a separate pod
# Cosmos
Pros of using cosmos:
- Each task (each table to build) is separated from others, we can assign to it different resources and retry it in case of failure without restarting the rest of models dbt builds

Cons of using cosmos:
- If we have a lot of dbt models we can end up with a lot of pods what can be problematic to manage

We can create different task groups by using dbt tags and create for example group with dbt models which require more computational power and assign to pods for those tasks more resources.