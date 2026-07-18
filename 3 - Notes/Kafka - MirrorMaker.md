Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Kafka MirrorMaker is a tool used to replicate data between Kafka clusters. It copies topics and messages from one cluster to another.

Common use cases:
- Disaster recovery (keeping a copy of a cluster in case we loose one)
	- It can be useful for example for such cases as:
		- entire data center outage
		- cloud region failure
		- major configuration mistake
		- accidental deletion of topics
		- corrupted data
		- security incident
- Multi-region deployments (deploying clusters in different part of the World)
	- So that users in different parts of the World have clusters they use closer to them