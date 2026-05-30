Tags: [[__Machine_Learning_Engineering]] [[_Milvus]]
#MLEngineering #Milvus 

# Introduction
When we insert new entities into a collection using the `collection.insert(entities)` command, then this data is saved only in memory.

If we want to write this data to the persistent storage (on a disk), then we need to additionally use the flush function: `collection.flush()`.

If we use only `collection.insert()` and we don’t use the `collection.flush()`, and the script exits, then data will be lost.