Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Schema Registry is a service that stores and manages schemas ([[Kafka - Schema|link]]) for Kafka messages. 

It stores schemas separately from Kafka messages and help producers and consumers serialize/deserialize messages consistently.

It helps ensure that producers and consumers agree on the message format.

It commonly works with serialization / schema validation formats ([[Software Engineering - Serialization|link]] / [[Software Engineering - Schema definition (validation) formats|link]]):
- Avro
- Protobuf
- JSON Schema
# Schema
A schema in this case is a definition of the data structure that tells applications how to encode and decode the message.
# How it works
## 1. Producer sends a message
Suppose you have a `users` topic.

Your application has an object:
```
{
  "id": 123,
  "name": "Alice"
}
```

You define a schema:
```
User:
- id: integer
- name: string
```

The producer sends:
```
Message:
    schema ID: 5
    data: <binary encoded data>
```

It does not send the whole schema every time.

Instead:
```
Kafka message:

[Schema ID = 5][Encoded data]
```
## 2. Schema Registry stores the schema
Before sending, the producer checks:
```
"Do I already have this schema?"
```

If not:
```
Producer
    |
    v
Schema Registry

Store:
Schema ID: 5

User:
- id: integer
- name: string
```

Now the schema has an ID.
## 3. Kafka stores only the message
Kafka stores:
```
Topic: users

Message:
Schema ID: 5
Data:  <binary data>
```

Kafka itself does not understand:
- `id`
- `name`
- integer
- string

Kafka just stores bytes.
## 4. Consumer reads the message
Consumer receives:
```
Schema ID: 5
Data
```

It asks Schema Registry:
```
"Give me schema 5"
```

Schema Registry returns:
```
User:
- id: integer
- name: string
```

Now the consumer can deserialize:
```
binary data
        |
        v
User object

{
  id: 123,
  name: "Alice"
}
```
