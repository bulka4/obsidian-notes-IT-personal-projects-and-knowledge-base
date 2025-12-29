Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Hadoop setup
## The best materials:
- [youtube - Data Engineering](https://www.youtube.com/watch?v=_iP2Em-5Abw) - multi node hadoop set up without docker
- [www.cloudduggu.com](https://www.cloudduggu.com/hadoop/installation-multi-node-cluster/) - multi node hadoop set up without docker
- [www.michael-noll.com](#formatting-the-hdfs-filesystem-via-the-namenode) - multi node hadoop set up without docker
- [www.confessionsofadataguy.com](https://www.confessionsofadataguy.com/create-your-very-own-apache-spark-hadoop-cluster-then-do-something-with-it/) - Setup of both Hadoop and Spark. there is no info about on which nodes (servers) execute which commands in terminal for setting up hadoop. But the part for Spark seems fine.

## Official documentation:
- Hadoop official documentation about cluster setup: [hadoop.apache.org](https://hadoop.apache.org/docs/r2.8.0/hadoop-project-dist/hadoop-common/ClusterSetup.html)
- Hadoop official HDFS guide: [hadoop.apache.org](#Related_Documentation)

## Other materials:
- [medium.com](https://freedium.cfd/https:/blog.det.life/developing-multi-nodes-hadoop-spark-cluster-and-airflow-in-docker-compose-part-1-10331e1e71b3) - medium article about multi node hadoop and spark set up with docker. It creates multiple data nodes as separate docker containers but everything is running on a single machine using docker compose.
- [medium.com](https://freedium.cfd/https:/medium.com/@rubenafo/some-tips-to-run-a-multi-node-hadoop-in-docker-9c7012dd4e26) - hadoop multi node set up. There is a missing piece about generating ssh keys. Here different data nodes are created in a separate docker containers and all of them are running on a single machine. Docker compose is not used so some additional task related to networks in Docker are required.
- [linkedin.com](https://www.linkedin.com/pulse/setup-multi-node-hadoop-cluster-using-docker-komal-suthar/) - hadoop multi node set up. Some actions are done with docker, some manually.
# Theory
- [youtube - Data Engineering](https://www.youtube.com/watch?v=N6TmDNexxGI&list=PLGhXxbu7qYooyn_aWk1DqpIF1CjBzaSUn&index=2) – Hadoop theory
- [youtube - Data Engineering](https://www.youtube.com/watch?v=rsOSrEbK7sU&list=PLLa_h7BriLH1OE82WZOH534WufJq824mb) – The entire playlist about Hadoop
- [youtube - Data Engineering](https://www.youtube.com/watch?v=Tyg1FVNq40g&list=PLGhXxbu7qYooyn_aWk1DqpIF1CjBzaSUn&index=3) - Hadoop and Spark (9h video)

#DataEngineering #DistributedComputing 