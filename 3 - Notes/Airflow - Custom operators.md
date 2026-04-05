Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
We can create a custom Airflow operator by creating a class which extends the Airflow's `BaseOperator` class.

For example, instead of creating a function and running it as a task using `PythonOperator`:
```python
import requests

def call_api():  
	r = requests.get("https://api.example.com/data")  
	print(r.json())  
  
task = PythonOperator(  
	task_id="call_api",  
	python_callable=call_api,  
)
```

we can create a custom operator like that:
```python
from airflow.models import BaseOperator  
import requests  
  
class SimpleApiOperator(BaseOperator):
  
	def __init__(self, url, **kwargs):  
		super().__init__(**kwargs)  
		self.url = url  
	  
	def execute(self, context):  
		response = requests.get(self.url)  
		data = response.json()  
  
		self.log.info(f"Response: {data}")  
		return data
```

and use it in DAG like that:
```python
task = SimpleApiOperator(  
	task_id="get_data",  
	url="https://api.example.com/data"  
)
```

So in the operator class we need to define the `execute` function and only that function will be executed when using the operator in an Airflow DAG.
# Operator's init function
Operator's init function runs during DAG parsing, not during task execution. If we create some variables needed for task execution, it is better to create them in the `execute` function.

For example, when we want to create Kubernetes resources and we load configs and create a client for doing this:
```python
# create configs with credentials used for authentication when making Rest API calls to Kubernetes API
config.load_incluster_config()
# Create Kubernetes API client to work with jobs (by making a Rest API call to Kubernetes)
batch_v1 = client.BatchV1Api()
# Create Kubernetes API client to work with pods (by making a Rest API call to Kubernetes)
v1 = client.CoreV1Api()
```
