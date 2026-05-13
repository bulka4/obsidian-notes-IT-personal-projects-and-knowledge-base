Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

## Dockerfile
In the Dockerfile we install tools needed for our DAGs:
- **Microsoft ODBC driver 18** - Needed for connecting to SQL databases from DAGs using SQLAlchemy library.
- **Python libraries** - We are installing all the required Python libraries ([[MS SQL - Data Lake data ingestion with Airflow project - Python libraries required for DAGs|link]]) from the requirements.txt file which will be used in DAGs.

We are installing all those tools by executing bash scripts using the 'RUN' command in the Dockerfile.
## Docker compose
We are using the official Airflow Docker compose file as described here: [airflow.apache.org](https://airflow.apache.org/docs/apache-airflow/2.6.0/howto/docker-compose/index.html).

In that Docker compose file we just need to comment out the line about image and uncomment the line about build:
```yaml
# image: ${AIRFLOW_IMAGE_NAME:-apache/airflow:2.6.0}
build: .
```
That's because we want to extend the basic Airflow image using the Dockerfile.