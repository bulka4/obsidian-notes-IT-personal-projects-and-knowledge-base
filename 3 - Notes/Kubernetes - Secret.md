Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Secret is a resource like ConfigMap but for storing confidential data.

We use this command to create a secret:
- Kubectl create secret \<type\> \<name\> [options]

Using this command we can:
- Define a secret value during executing this command
- Read secret value from a file
- Create a secret for a specific container registry which can be used for pulling images from it. It generates a new secret value based on credentials to a container registry which we pass in that command.
- Get TLS key and certificate from files.

#Cloud #DevOps #DistributedComputing #DataEngineering 