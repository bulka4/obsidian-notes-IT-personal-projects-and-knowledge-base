Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction

Azure DevOps is a service used for:
- Creating repositories with code
- Creating CI/CD pipelines
- Collaborating with a team (creating tasks, assigning them to people etc.)

In this document we are gonna focus on CI/CD pipelines.

# Agents

An Agent is a tool which performes actions defined in our CI/CD pipeline.

There are two types of agents:
- Self Hosted
	- We install them by ourself on our own server
- Microsoft-hosted (or just Hosted)
	- They are managed by Microsoft, installed on their servers

For example an Agent can perform the following actions:
- Build a Docker image using code from a repository
- Push a Docker image to a container registry
- Pull a Docker image from a container registry
- Run a container on the server using the pulled Docker image
- Execute any bash command

For this scenario better will be a Self Hosted Agent.

We can install that Agent on the server where we want to run our Docker image and all the above actions will be executed by that Agent on this server.

If we would like a Hosted Agent to pull an image onto our own server, then that Agent would need to connect to our server through SSH and execute proper commands there.

## Agent Pool

Agent Pool is a place where we are adding Agents.

Before we install a Self Hosted Agent on a server, we need to have prepared a Pool where we will add it.

# YAML pipeline definition

We can define our CI/CD pipeline as a YAML file which describes all the steps that need to be performed.

# DevOps Library

It is a service for storing confidential data. That data can be used in CI/CD pipelines.

## Variable groups

In DevOps Library we can create there Variable groups which contains variables which holds confidential data.

In a YAML file defining our CI/CD pipeline we can specify from which Variable groups we want to get data. Then we can access values of the variables from that group in that YAML file.

Here is an example of a YAML file which loads a Variable group given with name \<variable-group-name\> and we are using variables \<VARIABLE1\> and \<VARIABLE2\> from that group in a bash script which will be executed:
![[2 - Images/CI-CD pipelines in Azure DevOps/Screenshot 1.png]]

# Service connection

It is a tool allowing to connect to external systems from a DevOps CI/CD pipeline.

For example, in a YAML file defining our CI/CD pipeline we can specify that we want to use a specific connection in order to push a Docker image to a container registry.