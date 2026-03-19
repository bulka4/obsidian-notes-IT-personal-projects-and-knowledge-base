Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
Event-driven trigger is a mechanism that starts a DAG or task immediately when a certain event happens.

It is done by creating a program (separate than Airflow DAG) which waits for some event and starts Airflow DAG by using Airflow Rest API.
# Comparison to Airflow sensors
A difference between an event-driven trigger and Airflow sensor is that Airflow sensor:
- Is defined in a DAG
- DAG is started
- Sensor task in this DAG waits until a condition is satisfied
- DAG continues with further tasks
- Once tasks are finished, the entire DAG is finished and sensor doesn't wait for next events

while event-driven trigger:
- Is defined outside of a DAG
- Waits until a condition is satisfied
- Triggers a DAG