Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
We shouldn't be using `KubernetesPodOperator` together with the `KubernetesExecutor`. 

Both of them tries to create a new pod for running a task so it doesn't make sense to use them both together.