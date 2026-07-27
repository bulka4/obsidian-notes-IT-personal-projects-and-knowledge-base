Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Consensus is a mechanism that allows multiple nodes (servers) in a distributed system to agree on a single value or a decision, even when some nodes or a network fail, nodes can't communicate or some messages in an event-driven system ([[Backend Engineering - Event-driven architecture (EDA)|link]]) are delayed.
# Examples of what nodes can agree on
- What is the operation log ([[Backend Engineering - Distributed systems - State|link]]) (what operations were performed, in what order and what is the latest state).
- Data changes - Nodes agree on the order of data updates
- Configuration changes - Nodes agree on system settings, e.g. to use a specific version of a specific service
- Event ordering ([[Backend Engineering - Event-driven architecture (EDA)|link]]) - Nodes agree on the order of events
- Leader election - Nodes agree on who is the leader

Note that some aspects can be considered as an operation (e.g. configuration change) but sometimes they are not considered as an operation so that's why we say broader "decisions".
# Why is consensus needed?
Consensus algorithms are used to decide what is the official operation log ([[Backend Engineering - Distributed systems - State|link]]) (what operations were performed, in what order and what is the latest state).

For example, to avoid a problem where:
- Only one node applies and records a write
- That node crashes
- The remaining nodes don't know about the write - the system loses the official, true history about what operations were performed.

For example, that write could be changing a balance in a bank account. One node withdraws a 100 USD, that node crashes and the rest of the system doesn't know that a 100 USD were withdrawn.
# Example algorithms for implementing consensus
Algorithms for implementing consensus include:
- Raft
- Paxos

They solve problems like:
- Who is the leader?
- Which operation happened first?
- What data should be considered committed?
# Committing a change and a leader
Usually, one node is a leader and committing a change (performing a write, changing the state) is done in the following way:
- The client sends the write to the leader
- The leader appends the write to its log and forwards it to the follower nodes
- The followers append the write to their logs and acknowledge the leader
- Once the leader receives acknowledgements from a majority of nodes, it marks the write as committed
- The leader informs the followers that the write is committed, and they apply it to their state
## How a leader is elected
When a leader crashes, a new one needs to be elected:
- The new leader needs to have the latest committed state (the latest committed log entries)
- Nodes votes on who will be a new leader and a node with a majority of votes wins
- Before voting, each node checks whether the candidate's log is at least as up to date as its own. If not, it refuses to vote
- A node becomes a leader if it receives votes from a majority of nodes in the cluster
## Why majority needs to append a write to their log
When majority has the latest state, then we can be sure that the majority electing a new leader contains at least one node which has the latest state (the latest committed log entries)):
- We have two groups of nodes here:
	- A majority that has the latest state (stored the latest change)
	- A majority that votes for a new leader
- Since both groups are majorities:
	- there needs to be at least one common node in both groups
	- that one common node has the latest state and it voted on the new leader
	- so it guarantees that the new leader also has the latest state (because nodes doesn't vote on nodes which are missing some entries in the operation log), e.g.:
  ```
	A B C D E  <- 5 nodes
	A B C      <- One majority group
	C D E      <- Second majority group ("C" is a common node in both groups)
  ```
# Where is consensus used?
Examples:
- Leader election
- Distributed databases
- Configuration management
- Service coordination
# Related topics
- FLP impossibility - [[Backend Engineering - Distributed systems - FLP impossibility|link]] 