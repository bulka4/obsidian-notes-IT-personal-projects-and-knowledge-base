Tags: [[__My_projects]]
#MyProjects 

# Introduction
Additionally Terraform saves files on the host where we run Terraform code:
- Dockerfile:
    - Used to run a container with prepared environment to interact with AKS
    - Saved in the docker folder
- values.yaml x2:
    - Two values.yaml files used in Helm charts:
    - Saved in the mlflow_project and mlflow_setup folders in the docker > helm_charts folder.

In the template_files folder we have templates of those files. We will interpolate them (insert variables values) and save on the localhost.