Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
We can save artifacts by writing:
```python
with mlflow.start_run() as run:
    mlflow.log_artifact('graph.png')
```
It saves a local file `graph.png` as an artifact in the artifact store.

We should save it under the `start_run()` command to assign this artifact to a run like described here - [[MLflow - Attaching a python script to a run|link]].

Models and artifacts are saved there in the following structure:
```bash
|-- experiment_1_ID
	|-- run_1_ID
		|-- artifacts
		|-- metrics
		...
	|-- run_2_ID
	...
	|-- models
		|-- model_1_ID
		|-- model_2_ID
		...
|-- experiment_2_ID
...
```