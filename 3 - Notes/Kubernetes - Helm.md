Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Helm is a package manager for Kubernetes that helps you define, install, and manage Kubernetes applications.
## Sharing Helm charts
Helm uses charts, which are packages of pre-configured Kubernetes resources written in YAML. They can be uploaded and downloaded from repositories.
## Templating YAML files
Helm also allows for creating YAML files which are using variables and we can put different values into them.
## Example chart
**File structure**

Our chart might look for example like that:
![[2 - Images/Kubernetes/Screenshot 1.png]]

In the templates folder we have manifests (templates) of resources which we want to deploy.

**Chart.yaml**

In the Chart.yaml file we can specify dependencies, that is what other Helm charts we want to install except for resources from the templates folder. Here for example we install MySQL chart from the bitnami repository:
![[2 - Images/Kubernetes/Screenshot 2.png]]

**Values.yaml**

In the values.yaml file we are specifying variables which will be used in manifests in the templates folder.

For example we can have a variables like this:
```
mlflow:
	secretName: mlflow-secret
```

And refer to it in a manifest like this:
```
metadata:
	name: {{ .Values.mlflow.secretName }}
```

**Dependency parameters**

Also we can provide in the values.yaml values for parameters for installing dependencies. In our example we have MySQL as a dependency. We can provide values in the values.yaml for parameters for this dependency like this:
```
mysql:
	resourceName: mysql
	# storageSize: 8Gi
	primary:
		persistance:
			enabled: true
			existingClaim: mysql-pvc
			storageClass: ""
```
 

Here the name ‘mysql’ needs to be the same as name of the dependency.

That will be equivalent to installing MySQL using Helm this way:
![[2 - Images/Kubernetes/Screenshot 3.png]]
## Helpers
Helpers are named templates which allow us to create named configurations which we can use in our YAML files by using their name.

Helpers are defined in the templates/_helpers.tpl file.

For example we can define a helper like this:
![[2 - Images/Kubernetes/Screenshot 4.png]]

That created a helper called ‘mlflow-job.labels’ and its content are those two lines between {{-define .. -}} and {{- end }} blocks.

And use it in a YAML file like this:
![[2 - Images/Kubernetes/Screenshot 5.png]]

So in place of a helper name will be inserted its content like this:
![[2 - Images/Kubernetes/Screenshot 6.png]]


#Cloud #DevOps #DistributedComputing #DataEngineering 