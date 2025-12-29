Tags: [[__Data_Engineering]]

# Introduction
There are a few options for deploying Airflow:
- Azure Data Factory
- Google Cloud Composer
- MWAA
- Astronomer
- Docker / Kubernetes

Azure Data Factory, Google Cloud Composer and MWAA are simple to use but there is a lot of limitations, you can’t modify too much the environment in which Airflow is running. For example you can’t install additional tools needed for Airflow dags like database drivers.

Astronomer offers much more flexibility. You can modify there Docker images which prepares environment in which Airflow is running.

Ranking of solutions according to flexibility:
1. VM
2. Docker / Kubernetes serverless services
3. Astronomer
4. ADF / GCC / MWAA

Ranking of solutions according to simplicity of usage:
1. ADF / GCC / MWAA
2. Astronomer
3. Docker / Kubernetes serverless services
4. VM

#DataEngineering 