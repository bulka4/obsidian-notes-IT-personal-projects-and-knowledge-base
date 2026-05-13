Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
In this repository we have:
- Terraform scripts for creating Linux VMs in Azure.
- Bash scripts for setting up HDFS, YARN, Spark and Jupyter Notebook on those VMs. 

We will create two Linux VMs which:
- Will act as a master and a slave node
- We will be able to connect to using SSH

We will be able to:
- Access a Jupyter Notebook through a browser from our local computer and run Spark code from it.
- Review data in HDFS UI
# Code repository
Repository with the code: [github.com](https://github.com/bulka4/hadoop_spark).
# Repository guide
Here is a guide describing how to use this code - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Repository guide|link]].
# Prerequisites
Prerequisites we need to satisfy before start using the code from this repository - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Prerequisites|link]].
# Code explanation
- Creating Azure resources with Terraform - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Creating Azure resources with Terraform|link]] 
- Configuring VMs using bash scripts - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Configuring VMs using bash scripts|link]] 
- Network security rules - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Network security rules|link]] 
- Terraform outputs - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Terraform outputs|link]] 
- SSH key generation - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - SSH key generation|link]] 
- Hadoop setup - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Hadoop setup|link]] 
# Problems and ideas for improvements
Problems and ideas for improvements - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Problems and ideas for improvements|link]].