Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Common deployment options:
# Local / Development
- Kafka usually runs as one or a few processes on a local machine
- Processes we run:
	- Kafka broker
	- KRaft controller
# Distributed
Processes we run:
- Controller nodes (multiple)
- Broker nodes (multiple)
## Kubernetes
To deploy on Kubernetes ([[Kafka - Kafka on Kubernetes|link]]) we can use:
- Strimzi
- Confluent Operator
- Helm charts