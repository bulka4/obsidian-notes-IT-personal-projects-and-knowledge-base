Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Introduction
Graceful shutdown means stopping a service in an orderly way instead of killing it immediately.

The goal is to let the application finish or clean up work that is already in progress.

For example:
```
Shutdown requested
       ↓
Stop accepting new requests
       ↓
Finish requests already being processed
       ↓
Finish/clean up background work
       ↓
Close DB connections, Kafka consumers, files, etc.
       ↓
Exit process
```
