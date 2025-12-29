Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Operators can manage applications (resources) in Kubernetes. For example, in case of PostgreSQL it can:
- Create a PostgreSQL instance
- Monitor its health
- Automatically handle failures
- Manage backups

Or in case of Spark Operator:
- It watches for the SparkApplication custom resource
- Once that resource is created it creates a Spark Driver Pod

Or it can:
- Watch for MySQL secret to be created
- Once it is created Operator fetches a value from this secret and saves it in another secret

#Cloud #DevOps #DistributedComputing #DataEngineering 