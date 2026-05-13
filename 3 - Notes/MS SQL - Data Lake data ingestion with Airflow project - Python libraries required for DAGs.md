Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
In the `requirements.txt` we are specifying all the Python libraries which are needed to run our DAGs.

It is a good practice to include in that file a version of airflow which we want to use, for example: `apache-airflow==2.6.0`:
- That's because other libraries might be in conflict with the airflow version which we want to use and this way we will see logs about that. 
- Otherwise airflow version might be changed automatically. 

Also it is good to include `apache-airflow` in the `requirements.txt` file when we are developing code which we will want to run later on using Airflow.