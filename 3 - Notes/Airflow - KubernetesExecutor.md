Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
With KubernetesExecutor, each task runs in its own Kubernetes pod. 

That pod, by default, will use the Airflow worker image (the one from the Helm repo). If we want to use a different image, we need to use the KubernetesPodOperator ([[Airflow - KubernetesPodOperator|link]]).