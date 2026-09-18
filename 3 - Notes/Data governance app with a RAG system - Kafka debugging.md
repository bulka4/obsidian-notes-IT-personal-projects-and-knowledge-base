Tags: [[__My_projects]]
#MyProjects 

## Check connectivity to Kafka
Using:
```shell
kubectl -n semantic-search exec -it kafka-controller-0 -- \
	kafka-broker-api-versions.sh --bootstrap-server localhost:9092
```
works so Kafka is reachable.

In Python consumer's logs, we saw:
```
Sent FindCoordinatorRequest
Received FindCoordinatorResponse
COORDINATOR_NOT_AVAILABLE
```
so that also confirms that connectivity to Kafka works.
## Produce a message and save it in a topic
The topic is healthy, we checked it using:
```shell
kubectl exec -it kafka-controller-0 -- \
	kafka-topics.sh \
	--bootstrap-server kafka:9092 \
	--describe --topic table-descriptions
```

We tried to produce a message and save it in a topic:
```shell
kubectl -n semantic-search exec -it kafka-controller-0 -- \
	kafka-console-producer.sh \
	  --bootstrap-server localhost:9092 \
	  --topic table-descriptions
	  
# After executing the above comand, enter the below value, press Enter and then
# ctrl + c
{"event_type":"table_description_created","table_id":"12345"}
```

and it worked. Running:
```shell
kubectl -n semantic-search exec -it kafka-controller-0 -- \
	kafka-get-offsets.sh \
	  --bootstrap-server localhost:9092 \
	  --topic table-descriptions
```
shows that there are messages in the topic:
```
table-descriptions:0:5
```
## Consuming messages
Consuming messages using `kafka-console-consumer.sh` and a specific offset works:
```shell
kubectl -n semantic-search exec -it kafka-controller-0 -- \
	kafka-console-consumer.sh \
	  --bootstrap-server localhost:9092 \
	  --topic table-descriptions \
	  --partition 0 \
	  --offset 0
```
but without specifying an offset, it doesn't consume any messages.
## Consumer group
Running:
```shell
kafka-consumer-groups.sh --list
```

shows no `embedding-ingestion-service` consumer group.

There are errors for this group, running:
```shell
kubectl -n semantic-search exec -it kafka-controller-0 -- \
	kafka-consumer-groups.sh \
	  --group embedding-ingestion-service \
	  --describe
```
shows:
```
TimeoutException
...
FIND_COORDINATOR
...
node 0 being disconnected
```

Python client's logs, from the embedding ingestion service, also shows:
```
Group "embedding-ingestion-service":
FindCoordinator response error:
COORDINATOR_NOT_AVAILABLE
```

Probably Python consumer has not successfully joined the consumer group.
## Kafka's internal `__consumer_offsets` topic
consumer groups store their offsets in Kafka's internal topic `__consumer_offsets` and it is not present when checking with:
```shell
kubectl -n semantic-search exec -it kafka-controller-0 -- \
	kafka-topics.sh \
	  --bootstrap-server localhost:9092 \
	  --list
```

also, describing this topic shows nothing:
```shell
kubectl -n semantic-search exec -it kafka-controller-0 -- \
	kafka-topics.sh \
	  --bootstrap-server localhost:9092 \
	  --describe \
	  --topic __consumer_offsets
```

Trying to recreate this topic using:
```shell
kubectl -n semantic-search exec -it kafka-controller-0 -- \
	kafka-topics.sh \
		--bootstrap-server localhost:9092 \
		--create \
		--topic __consumer_offsets \
		--partitions 50 \
		--replication-factor 1
```
succeeds and creates the topic. 

After creating this topic, the Python clients doesn't through the `COORDINATOR_NOT_AVAILABLE` error and it receives messages.
## Kafka's configuration
We are trying to set up those configs because we have a single broker:
```shell
offsets.topic.replication.factor=1
transaction.state.log.replication.factor=1
transaction.state.log.min.isr=1
```

Checking kafka settings:
```shell
kubectl exec -n semantic-search kafka-controller-0 -- \
  grep -E 'offsets.topic|transaction.state'  
	  /opt/bitnami/kafka/config/server.properties
```
shows nothing.

Checking those configs:
```shell
kubectl -n semantic-search exec kafka-controller-0 -- \
  kafka-configs.sh \
  --bootstrap-server localhost:9092 \
  --entity-type brokers \
  --entity-default \
  --describe | grep -E "offsets.topic|transaction.state"
```
shows nothing.
## Check Kafka pod logs
looking for errors in logs:
```shell
kubectl -n semantic-search logs kafka-controller-0 | \
  grep -i -E "consumer_offsets|replication factor|INVALID_REPLICATION_FACTOR|auto.create|failed"
```
shows no errors.
## Helm generated manifest
Test what YAML manifest Helm would generate:
```shell
helm template test . -f values.yaml | grep -i 'offsets'

helm template test . -f values.yaml | grep -E  'offsets\.topic|transaction\.state\.log'
```

It shows nothing.
## Helm values
Check what values from the `values.yaml` file were used:
```shell
helm get values kafka -n semantic-search --all
```

Check available values:
```shell
helm show values oci://registry-1.docker.io/bitnamicharts/kafka \
	--version 32.4.3 \
	| grep -i -A5 -B5 "overrideConfiguration"`
```
