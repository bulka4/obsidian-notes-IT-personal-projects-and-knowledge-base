Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction new
In this project, we create a multi-node Hadoop cluster from scratch on Azure Linux VMs allowwing for distributed storage and processing big amounts of data. The cluster consists of:
- HDFS
- YARN
- Spark

To set it up, we use:
- Terraform scripts for creating Linux VMs in Azure.
- Bash scripts for setting up HDFS, YARN, Spark and Jupyter Notebook on those VMs. 

We will be able to:
- Access a Jupyter Notebook through a browser from our local computer and run Spark code from it.
- Review data in HDFS UI
- Connect to VMs using SSH

**Architecture overview**
- We create a cluster consisting of 2 nodes - one acts as a master, another one as a slave.
- YARN is used as a scheduler for running Spark jobs.
- Jupyter Notebook is launched on the master node which allows for developing and running Spark code which can interact with HDFS.

**Implementation overview**
Hadoop cluster can be started by following steps below:
- Run Terraform code to:
	- Create two Azure Linux VMs
	- Execute on them bash scripts which configure both servers:
- Make preparations for Hadoop cluster
- Start Jupyter Notebook
- Connect to both VMs using SSH and run on them a few commands which start the cluster.

All of this can’t be done fully automatically using Terraform because it is necessary to run commands on both servers in a proper order.

This would require using a different tool, for example Ansible.
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
# Problems encountered during working on this project
Problems encountered during working on this project - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Problems encountered during working on this project|link]].
# Problems to solve and ideas for improvements
Problems and ideas for improvements - [[Multi-node HDFS, YARN and Spark cluster on Azure Linux VMs project - Problems and ideas for improvements|link]].