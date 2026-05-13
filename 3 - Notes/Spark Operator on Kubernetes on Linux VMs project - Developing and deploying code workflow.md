Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
To develop Spark code and run it in a cluster mode on Kubernetes we can:
- Develop and test code in Jupyter Notebook ([[Spark Operator on Kubernetes on Linux VMs project - Jupyter Notebook setup|link]])
	- We can connect to it remotely through a browser (from any machine) and run from it Spark in a local mode
- Run the prepared Spark code in a cluster mode using Spark Operator ([[Spark Operator on Kubernetes on Linux VMs project - Running Spark jobs with Spark Operator|link]])
# Mounting a volume with Spark code
To be able to develop scripts in Jupyter Notebook and run them using Spark operator we mount a shared volume:
- Mount a volume (a folder on the host) to the container running Jupyter Notebook
- Scripts developed in the Jupyter, are saved in this volume on the host
- Spark Operator creates a pod where scripts developed in Jupyter are mounted and executed