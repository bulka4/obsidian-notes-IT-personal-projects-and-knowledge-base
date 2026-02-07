Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
When installing a chart, we can also install other charts together with the main one by assigning them as dependencies.

In the `Chart.yaml` file we can specify what dependencies we want, for example when we have `Chart.yaml` like this:
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

it means that we will additionally install the `airflow` chart as a dependency using the chart from the repository `https://airflow.apache.org`.
# Parameters for dependencies
We provide parameters for dependency charts in a `values.yaml` file in a special way, what is described here - [[Helm - values.yaml]].