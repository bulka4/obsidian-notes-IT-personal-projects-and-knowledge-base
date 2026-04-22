Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Dynamic task generation
We can create tasks in Airflow dynamically by creating them in a loop:
```python
tables = ["users", "orders", "payments"]

for table in tables:
    process = PythonOperator(
        task_id=f"process_{table}",
        python_callable=process_table,
        op_args=[table],
    )
```
# Dynamic Task Mapping
We can use the Dynamic Task Mapping to create new tasks dynamically based on an output of an upstream task:
```python
@task
def get_tables():
    return ["users", "orders", "payments"]

@task
def process_table(table):
    print(table)

process_table.expand(table=get_tables())
```
The `expand` command causes that for every element from the output of the upstream task `get_tables`, a new `process_table` task is created which takes that output as an input, so in this case we get created 3 tasks:
- `process_table("users")`
- `process_table("orders")`
- `process_table("payments")`
