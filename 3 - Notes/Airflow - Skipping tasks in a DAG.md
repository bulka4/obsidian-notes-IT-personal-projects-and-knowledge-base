Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
In Airflow we can create a conditional task which decides whether or not to progress with further, downstream tasks in the DAG.

Below are explained two ways for doing this:
- Using the `ShortCircuitOperator` operator
- Using the `AirflowSkipException` Airflow exception
# `ShortCircuitOperator`
We can use the `ShortCircuitOperator` operator to create a conditional task which decides whether or not to progress with further, downstream tasks in the DAG.

We need to create a function which checks a condition and returns either true or false and use it in the `ShortCircuitOperator`:
```python
def check_condition(**kwargs):
    ...
    condition = x > 5
    return condition  # True or False value

# Task for checking whether or not we need to retrain the model
check = ShortCircuitOperator(
    task_id="check_condition",
    python_callable=check_condition
)

# Task to run if the condition is satisfied
task = <another-airflow-task>

# Run the task only if the `check` task returns True
check >> task
```
# `AirflowSkipException`
If our task code raises the `AirflowSkipException` exception, then this task and all the further, downstream tasks in the DAG are being skipped and their status is marked as skipped (not failed).

For example, we can use it in a custom operator ([[Airflow - Custom operators|link]]) like this:
```python
class MyOperator(BaseOperator):
	...
	def execute(self, context):
		condition = ... # True or False
		# Skip downstream tasks if the condition variable indicates to do so
        if condition:
            raise AirflowSkipException("Skipping downstream tasks")
```
