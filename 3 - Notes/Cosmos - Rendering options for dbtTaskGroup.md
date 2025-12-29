Tags: [[__Data_Engineering]]

# Introduction
For every task group created using the dbtTaskGroup we can define which dbt commands will be executed, for example we can only build models, or snapshots, or only perform tests.

We configure that using the render_config argument and the RenderConfig() function in the following way:
```
dbtTaskGroup(
	render_config=RenderConfig(
		argument_1=value_1
	)
)
```

Here are example arguments for the RenderConfig function:

· **select=["selector"]** - Use a node selector in order to build only a specific nodes (models, snapshots). For example a selector can be "path:" to build all the nodes from a folder at a given path (like 'models' or 'snapshots') or "model_name" to build a specific model.

· **exclude=["selector"]** - We are using here node selectors like in the select=["selector"] but it excludes specific nodes.

· **should_detach_multiple_parents_tests=True** - This argument makes sure that when we have models dependent on each other then we will not execute the same tests twice and when tests depends on a multiple models, then they will be performed when all those models have been built. Otherwise we might perform test which includes a model which has not been built yet and it will fail.

· **test_behavior="after_all"** - This argument causes that all tests will be performed after all the models have been built (there will be a single task in Airflow for testing).

#DataEngineering 