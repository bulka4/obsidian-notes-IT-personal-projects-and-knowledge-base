Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Protocol Buffers (Protobuf) is used to convert data into a binary format which has the following benefits compared other data formats:
- Uses much less memory (so sending over network is faster)
- Is faster to parse (read)
- Work across many different programming languages
# Where it is used
- Microservices communication - Especially with gRPC
- Internal backend systems - low latency services, high throughput systems
- Streaming / distributed systems - Kafka pipelines (sometimes)
# `.proto` file
A `.proto` file is used to define the structure of data. It is used when converting data into a binary format and back to other formats. It looks like that:
```
message User {
  int32 id = 1;
  string name = 2;
  int32 age = 3;
}
```
# schema evolution
Protobuf supports changing data safely, for example:
- we can add new fields
- old services ignore unknown fields

This is very important in distributed systems.
