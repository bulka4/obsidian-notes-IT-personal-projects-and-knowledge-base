Tags: [[__Data_Engineering]], [[__Distributed_computing]], [[_Spark]]

# Introduction
ApplicationMaster is a YARN process (daemon, Java process) needed to run Spark jobs. It is responsible for:
- Negotiating resources with the YARN ResourceManager
- Monitoring the job’s progress
- Handling task failures and retries

#DataEngineering #DistributedComputing #Spark