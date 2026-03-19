Tags: [[_My_projects]]
#MyProjects 

# Introduction
Data ingestion is performed using Python. Python script is ran in its own pod on Kubernetes created by the Airflow KubernetesPodOperator.
# Checking row counts
During every data ingestion, we check how many new rows we are ingesting. This can be used to detect issues, if one day we have significantly less or no new records, that might indicate some issue.