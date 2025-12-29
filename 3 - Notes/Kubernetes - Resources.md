Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
In Kubernetes we are creating resources which are objects with different purposes, which we manage and which helps us to manage our applications.

Those are tools used for running our application, for example we might have the following resources:
- Pod – containing a container running our app
- Service – Assigning a static IP address to the container running our app
- Volume – mounting external storage to the container running our app

More resources are mentioned and explained in further sections of this documentation.
## Manifests
Manifests are conifguration files (mainly YAML) which defines what resources we want to create in Kubernetes cluster.

We are preparing Manifest first and then we apply it in order to create the specified resource.
## Custom resources
Standard resources and available by default in every Kubernetes cluster and Custom resources are additional ones added by using the CRD (Custom Resource Definition) which is a YAML manifest specifying that resource.

#Cloud #DevOps #DistributedComputing #DataEngineering 