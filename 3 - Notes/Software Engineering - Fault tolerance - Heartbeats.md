Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Heartbeats are periodic signals sent by a component to indicate that it is still alive and functioning. Missing heartbeats allow other components to detect failures and take corrective actions.

The idea:
> "If I keep receiving heartbeats, the component is probably healthy. If heartbeats stop, it may have failed."

If other nodes stop receiving heartbeats from Node A, they may decide:
> "The leader has failed, we need to elect a new one."
# Common uses
- distributed systems
- cluster management
- leader election
- failure detection
# Difference from health checks

| |Health check|Heartbeat|
|---|---|---|
|Direction|System asks service|Service reports itself|
|Purpose|Verify health|Signal liveness|
|Example|Load balancer calls `/health`|Server sends "I am alive" message|
|Common use|Routing traffic, restarting containers|Distributed coordination|