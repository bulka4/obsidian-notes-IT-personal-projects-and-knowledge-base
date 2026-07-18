Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Serialization is a process of converting an object in memory (for example a Python object, data structures, numpy arrays, ML models) into a format that can be:
- Stored (in a file, DB, or memory store), or
- Transmitted (over a network), and
- Later deserialized back into the original object.

A format that is a result of serialization can be for example bytes, JSON, XML etc.

Common serialization types and formats:
- Binary serialization - Converting data into a binary representation (bytes):
	- Protobuf - [[Software Engineering - Protocol Buffers|link]] 
	- Avro - [[Software Engineering - Avro|link]] 