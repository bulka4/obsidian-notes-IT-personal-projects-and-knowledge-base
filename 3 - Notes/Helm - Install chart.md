Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Install helm chart (deploy all the templates). This command will deploy all the resources in the specified namespace and create it if it doesn’t exist yet:
```bash
helm install <release-name> ./path_to_chart_directory -n <namespace>
```
# Provide values for chart parameters
To provide values for chart parameters from the `values.yaml` file, we can use the `--set` flag:
```bash
helm install <release-name> ./path_to_chart_directory \
	--set param1=value1 \
	--set param2=value2 \
	...
```
