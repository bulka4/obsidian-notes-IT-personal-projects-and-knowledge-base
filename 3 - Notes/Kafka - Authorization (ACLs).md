Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Authorization (ACLs) in Kafka uses ACL ([[Backend Engineering - Security - ACL (Access Control List)|link]]) to control what an authenticated user or application is allowed to do.
# Flow
The flow is:
```
1. Authentication:
   "Who are you?"
        |
        v
2. Authorization:
   "What can you do?"
```

After Kafka knows the identity of a client, it checks its ACLs (Access Control Lists).
# Resources for which to define permissions
ACLs define permissions for resources such as:
- Topics
    - Read messages
    - Write messages
    - Create/delete topics
- Consumer groups
    - Read/commit offsets
- Clusters
    - Administrative operations
# Example
```
ACL:

Principal:
    User: app1

Resource:
    Topic: orders

Permission:
    WRITE
```

Meaning:
> `app1` is allowed to produce messages to the `orders` topic.