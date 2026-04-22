Tags: [[_My_projects]]
#MyProjects 

# Introduction
For now we don't perform data ingestion on this platform but everything is prepared to do so.

Data ingestion can be performed using Python which can run in its own pod on Kubernetes created by Airflow.

We can use for that the custom Airflow operator from the `airflow/dags/common/KubernetesJobOperator.py` script which runs a Kubernetes job.
# Checking row counts
During every data ingestion, we can check how many new rows we are ingesting. This can be used to detect issues, if one day we have significantly less or no new records, that might indicate some issue.