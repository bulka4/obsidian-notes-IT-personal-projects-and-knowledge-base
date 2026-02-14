Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
In the `values.yaml` file we can provide parameters for our chart.
# Parameters for dependencies
When our chart has some dependencies ([[Helm - Dependencies|link]]), for example:
```yaml
apiVersion: v2
name: Airflow
description: Helm chart for deploying Airflow
version: 0.1.0

dependencies:
  - name: airflow
    version: 1.18.0
    repository: https://airflow.apache.org
```

Then, in order to set up parameters for the `airflow` dependency, we need to provide them under the `airflow` key in the `values.yaml` file:
```yaml
# Parameters for the main chart
main:
	param1: ...
	...

# Parameters for the 'airflow' dependency chart
airflow:
	param1: ...
	...
```
# Parameters specified twice
If we specify the same parameters twice, for example:
```yaml
param1:
	param2: 
	
param1:
	param3:
```

Then only one section will take effect.