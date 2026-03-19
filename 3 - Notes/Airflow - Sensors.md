Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
A sensor is a special type of Airflow task that waits for a certain condition to be true before allowing the DAG to continue.

Instead of running a DAG on a fixed schedule (e.g., every day at 2 AM), a sensor waits for an external event, like a file arriving in storage, a new database row, or a model metrics threshold.

Once an event occurs, a DAG with a sensor starts next tasks, and once they are completed, the entire DAG is completed so sensor is not waiting for next events. The entire DAG needs to be triggered again.
# Event-driven triggers
A similar concept are event-driven triggers, more info about them is here - [[Airflow - Event-driven triggers]].