Tags: [[__Machine_Learning_Engineering]]

# Introduction
Head node’s role is to:
- Run the GCS (Global Control Store) – It keeps cluster metadata, task scheduling info, actor locations.
- Run Dashboard – Monitoring UI
- Run the global scheduler – It knows resources of nodes (RAM, CPU etc) and using this info it can decide on which node we should run a Worker process which will execute our code.

#MLEngineering 