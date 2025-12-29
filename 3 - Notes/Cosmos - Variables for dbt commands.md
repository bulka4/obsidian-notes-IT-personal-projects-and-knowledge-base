Tags: [[__Data_Engineering]]

# Introduction
If we want to use variables for running dbt commands, like 'dbt run --vars', then we can do it in the following way:
```
with DAG(
	...
	,params={"my_name": "your_name"}
) as dag:
	dbtTaskGroup(
		operator_args={
			"vars": '{"my_name": {{ params.my_name }} }'
		}
	)
```

#DataEngineering 