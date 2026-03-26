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
