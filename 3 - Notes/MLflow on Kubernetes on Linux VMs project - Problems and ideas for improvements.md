Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# DNS resolution
There is a problem with resolution of public and Services DNS names from inside of a Pod. Because of that communication with the MLflow Tracking Server might not work.

Symptoms:
- At the beginning, after cluster setup, we can't resolve public and Services DNS names from inside of a Pod. When we restart the coreDNS deployment, `kubectl -n kube-system rollout restart deployment coredns`, it starts working.
# Terraform code sometimes doesn't work
Sometimes not entire bash script is executed successfully on one of the VMs and we need to run the entire Terraform code again (I don't know why).
