Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Commands
- Check processed messages in a topic:
```shell
kafka-console-consumer.sh \
	--bootstrap-server localhost:9092 \
	--topic table-descriptions \
	--group <group-name> \
	--from-beginning
```
- Produce a message using Kafka:
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
- Check partition's offset:
	```shell
	kafka-get-offsets.sh \
		--bootstrap-server localhost:9092 \
		--topic table-descriptions
	```
	
	After sending a message, it should show `table-descriptions:0:1`
- Describe a consumer group (e.g. check its offset):
	```shell
	kafka-consumer-groups.sh \
		--bootstrap-server localhost:9092 \
		--group <group-name> \
		--describe
	```