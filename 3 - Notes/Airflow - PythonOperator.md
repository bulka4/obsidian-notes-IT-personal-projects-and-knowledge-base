Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
The PythonOperator tool can be used to run a Python function as a task in a DAG. We use it in the following way:
```python
with DAG(
    ...
) as dag:

    def func():
        ...

    submit = PythonOperator(
        task_id="run_python_function",
        python_callable=func,
    )
```
The `submit` is an Airflow task which runs our Python function.