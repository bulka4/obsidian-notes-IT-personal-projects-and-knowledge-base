Tags: [[__Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
For Kafka messages we could define a schema using a JSON file, for example:
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "DocumentationUpdated.v1",
  "type": "object",
  "required": [
    "event_type",
    "document_id",
    "version",
    "updated_at"
  ],
  "properties": {
    "event_type": {
      "type": "string",
      "const": "DocumentationUpdated"
    },
    "document_id": {
      "type": "integer"
    },
    "version": {
      "type": "integer",
      "minimum": 1
    },
    "updated_at": {
      "type": "string",
      "format": "date-time"
    }
  },
  "additionalProperties": false
}
```

this specifies what fields must exists in every `DocumentationUpdated.v1` event.

The producer can validate messages against the schema when emitting an event and also the consumer can validate it when processing an event.
# Versioning
We could create different versions of message schemas. When we want to change a message schema, for example change `document_id: integer` into `document_id: string`, we can keep both schemas as different versions, to keep track of changes.

If we have different schemas for different messages, with different offsets:
```
offset 100 → DocumentationUpdated v1
offset 101 → DocumentationUpdated v2
offset 102 → DocumentationUpdated v2
```
then having saved different schema versions allows us to verify schema of all those messages.
# Schema registry
We could use a schema registry to manage schema files. The registry stores schemas and can enforce compatibility rules.
# Testing a producer and consumer
When we have a contract defined, we can test a producer and consumer independently.

We can:
- check whether the event emitted by the producer satisfies the contract, without a consumer processing it
- check whether the consumer can process a message that satisfies the contract, without emitting that message by the producer