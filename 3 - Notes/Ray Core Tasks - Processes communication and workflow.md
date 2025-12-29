Tags: [[__Machine_Learning_Engineering]]

# Introduction
When we run a task (using .remote()), then:
- Local Raylet (running on the same host where we run the task) tries to find a Worker process running on the same node as the Raylet which can execute the task.
- If there is no existing Worker process available for this task, then Raylet tries to create a new one (on the same node as the Raylet is running on).
- If the node where this Raylet is running on doesn’t have enough resources for creating a new Worker process, then Raylet asks the Cluster Scheduler to find a proper node.
- Cluster Scheduler finds a node with enough resources and talks to the Raylet running on this node to start the Worker proces.
- After executing the task, the Worker process becomes idle and can be reused for the future tasks.

Important features of the Raylet process:
- Raylet can run a Worker process only on the same host where Raylet is running.

Important features of the Worker process:
- It is not tied to one Task. Each Worker process can execute any task.

#MLEngineering 