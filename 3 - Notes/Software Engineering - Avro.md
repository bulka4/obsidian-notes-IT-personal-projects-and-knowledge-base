Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Apache Avro is a binary serialization format used to encode structured data into bytes.

It defines data using a schema:
```
User schema:

id: int
name: string
```

Schema is used to:
- serialize data during writing:
```
Object
  ↓
Avro serialization
  ↓
Binary bytes
```
- and deserialize it during reading:
```
Binary bytes
  ↓
Avro schema
  ↓
Object
```