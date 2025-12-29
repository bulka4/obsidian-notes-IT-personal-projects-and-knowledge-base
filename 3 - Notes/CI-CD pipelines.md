Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction

CI/CD pipeline is automated process which deploys code from a repository.

For example we can create a CI/CD pipeline which builds and pushes a Docker image to a container registry. It can work like this:
- Wait until someone pushed a commit to the repo
- Once commit is pushed, build a Docker image using code from the repo
- Push built Docker image to a container registry

Or we can create a pipeline which pulls a Docker image from a container registry and runs it on a server. It can work like this:
- Wait until a Docker image is pushed to a container registry
- Once a new Docker image has been pushed, pull it onto a server and run it.

A CI/CD pipeline can perform all the actions defined in it by using special functions provided by the tool which we are using for building that pipeline.

Popular tools for building CI/CD pipelines are:
- Azure DevOps (Azure Pipelines)
- GitHub Actions
- Jenkins

Popular functions which we can use in a CI/CD pipeline includes:
- Build a Docker image using code from a specific repo and push it to a container registry
- Execute a bash script

# YAML definition

We can define a CI/CD pipeline as a YAML file. We define there all the steps which needs to be done in a pipeline.