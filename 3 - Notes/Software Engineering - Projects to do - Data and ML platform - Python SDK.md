Tags: [[_Obsidian]] [[_Software_Engineering]]
#Obsidian #SoftwareEngineering 

# Introduction
Add a Python SDK allowing to interact with the platform. This demonstrates:
- package design
- API design
- OOP
- abstractions
# Pipeline execution
Instead of:
- triggering DAGs manually
- calling REST APIs

You do:
```python
client.pipelines.run("spark-etl")
```
# B) Dataset management
```python
dataset = client.datasets.create(
	"users-data"
	,path="s3://..."
)
client.datasets.version(dataset.id)
```

Think:
- data ingestion tracking
- dataset versioning
- lineage hooks
# C) ML training & tracking (MLflow abstraction)
Instead of using MLflow directly:
```python
client.experiments.start("fraud-detection")
with client.run():
    model = train()
    client.log_metrics({"accuracy": 0.92})
```
# D) Model registry + deployment
```python
model = client.models.register(run_id="123")client.deploy(
	model
	,environment="staging"
)
```

This abstracts:
- MLflow registry
- Kubernetes deployment
- Docker image building