Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Disaster recovery (DR) is the process of preparing for and recovering from major failures that make a system unavailable or cause data loss.

In Kafka, DR means ensuring that messages and services can continue working if the main Kafka environment fails.
# Common approaches

## 1. Replication inside a cluster
Protects against broker failures. When one broker fails, Kafka continues working.
## 2. Replication between clusters
Protects against cluster-level failures (when entire cluster goes down, we can use a `MirrorMaker` to make a backup ([[Kafka - MirrorMaker|link]])):

Used for:
- data center failure
- cloud region failure
- large infrastructure problems
## 3. Backups and recovery procedures
Examples:
- storing important data in external storage
- keeping topic configurations
- documenting how to recreate the cluster
# Important DR concepts
## RPO (Recovery Point Objective)  
How much data loss is acceptable. For example:
- RPO = 5 minutes → losing up to 5 minutes of messages is acceptable
## RTO (Recovery Time Objective)  
How quickly the system must recover. For example:
- RTO = 1 hour → system must be back within 1 hour