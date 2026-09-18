Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Check if producers can send messages and consumers receive them
- Check if a topic is healthy:
	```shell
	kubectl exec -it kafka-controller-0 -- \
		kafka-topics.sh \
		--bootstrap-server kafka:9092 \
		--describe --topic table-descriptions
	```
- Try to process messages in a topic:
	```shell
	kafka-console-consumer.sh \
		--bootstrap-server localhost:9092 \
		--topic table-descriptions \
		--from-beginning \
	    --offset 0
	```

- Produce a message and save it in a topic:
  ```shell
	kafka-console-producer.sh \
	  --bootstrap-server localhost:9092 \
	  --topic table-descriptions
	  
	# Enter the below value
	hello
  ```
- connect to a Kafka broker, to test connectivity to it:
  ```shell
  kafka-broker-api-versions.sh \
	  --bootstrap-server localhost:9092
  ```
- Check partition's offset (also indicating whether there are any messages):
	```shell
	kafka-get-offsets.sh \
		--bootstrap-server localhost:9092 \
		--topic table-descriptions
	```
- List consumer groups:
  ```shell
  kafka-consumer-groups.sh --list
  ```
- Describe a consumer group (e.g. check its offset):
	```shell
	kafka-consumer-groups.sh \
		--bootstrap-server localhost:9092 \
		--group <group-name> \
		--describe
	```
# Kafka config files
- Config file: `/opt/bitnami/kafka/config/server.properties`
- Check configs:
  ```shell
  kafka-configs.sh \
	  --bootstrap-server localhost:9092 \
	  --entity-type brokers \
	  --entity-default \
	  --describe | grep -E "offsets.topic|transaction.state"
  ```
# Python `confluent_kafka` library
When using the `confluent_kafka` Python library, we can use for debugging:
- Print additional logs:
  ```python
	from confluent_kafka import Consumer
	
	def error_callback(error):
        print(f"Kafka error callback: {error}", flush=True)
	
	consumer = Consumer({
		...
		# For debugging
		"debug": "broker,protocol,cgrp",
		"error_cb": error_callback,
	})
  ```
- 