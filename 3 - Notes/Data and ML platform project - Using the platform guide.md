Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Accessing services UIs
We can access UIs of different services by using below URLs in a browser:
- Airflow UI - `localhost:8080`
- MLflow Tracking server UI - `localhost:5000`
# Data transformation
For information about data transformation, including:
- Running SQL queries using Spark Thrift Server
- Building tables with dbt
refer to the documentation about data transformation - [[Data and ML platform project - Data transformation workflow (dev, kind)]].
# Train, evaluate and save ML models
How to train, evaluate and save ML models is described here - [[Data and ML platform project - Training, evaluating and saving ML models with MLflow]].
# Make and save predictions
For making and saving predictions we can use two scripts:
- `/apps/airflow/dags/make_predictions/make_predictions_spark_operator.py` - to be ran with Spark Operator
- `/apps/airflow/dags/make_predictions/make_predictions.py` - to be ran without Spark Operator, using Python

How they work and how to use them is described here - [[Data and ML platform project - Making and saving predictions]], in the 'Testing code' section.
# Example workflow
- Using dbt, build tables representing data from external sources and other tables using them as described in the 'Build tables using data from source1 and source2 sources' section here - [[Data and ML platform project - Data transformation workflow (dev, kind)|link]].
- Train ML model and save it the registry using prepared data as described here - [[Data and ML platform project - Training, evaluating and saving ML models with MLflow|link]], in the section 'Running and developing code'
- Run the Airflow DAG to make and save predictions as described here - [[Data and ML platform project - Making and saving predictions - Airflow orchestration|link]].
- Using dbt, build tables for ML model performance metrics as described here - [[Data and ML platform project - Data transformation workflow (dev, kind)|link]], in the 'Build tables with ML metrics' section