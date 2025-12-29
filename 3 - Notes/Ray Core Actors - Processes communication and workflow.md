Tags: [[__Machine_Learning_Engineering]]

# Introduction
Here is described which processes performs which tasks and how they communicate with each other.

When we create an Actor in our code, then:
- Local Raylet (running on the node where we run our code) tries to create on the local node a Worker process which will be assigned to this Actor (it will be running the code when we will call this Actor’s methods).
- If the local node doesn’t have enough resources, then Raylet asks the Cluster Scheduler to find a proper node
- Cluster Scheduler finds a node with enough resources to run the Worker process and talks to the Raylet from this node to run the Worker process.

When we call an Actor’s method in our code, then:
- We talk to the local Raylet (running on the same node where we run our code)
- If this Raylet is not the one managing this Actor, then it forwards the task (of executing the Actor’s method) to the Raylet from another node which does manage this Actor (each Raylet uses GCS to find out which Raylets manages which Actors)
- Raylet managing the Actor forwards the task to the Worker process assigned to this Actor. This Worker process runs on the same node as the Raylet.
- Worker process executes the task

Important features of the Raylet:
- Each Raylet uses GCS to find out which Raylets manages which Actors. In GCS there is metadata about it.
- Raylet which manages an Actor sends to the Worker process assigned to this Actor tasks of executing the code
- Raylet sends tasks only to Worker processes running on the same node as the Raylet

Important features of Worker processes assigned to Actors:
- They are long running processes, they run until we kill them.
- They execute code when we will call this Actor’s methods.
- They receive tasks to execute from the local Raylet running on the same node.
- Each Actor has assigned a single Worker process.

#MLEngineering 