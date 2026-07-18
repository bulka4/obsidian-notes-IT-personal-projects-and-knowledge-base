Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
To deploy on Kubernetes we can use:
- Strimzi
- Confluent Operator
- Helm charts
# 1. Strimzi
An **operator** for running Kafka on Kubernetes.

It provides custom resources like:
```
kind: Kafka
kind: KafkaTopic
kind: KafkaUser
```

You define Kafka as YAML manifests, and Strimzi creates/manages brokers, storage, upgrades, etc.
# 2. Confluent Operator
Also a Kubernetes operator, but developed by Confluent.

It can manage:
- Kafka
- Schema Registry
- Kafka Connect
- ksqlDB
- Control Center

It is more enterprise-oriented.
# 3. Helm charts
A generic Kubernetes packaging mechanism, not Kafka-specific.

A Helm chart is basically a collection of Kubernetes templates.

Example:
```
helm install kafka bitnami/kafka
```

Helm simply deploys resources.

It usually does not provide the advanced automation that operators do (automatic rebalancing, upgrades, managing topics/users, etc.).