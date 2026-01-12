Tags: [[__Machine_Learning_Engineering]], [[_Ray]]
#MLEngineering #Ray 

# Introduction
On every node we have the following processes running:
- Raylet - [[Ray - Raylet|link]]
	- Responsible for scheduling, launching and managing tasks/actors on the node where it runs.
- Plasma object storage - [[Ray - Plasma object storage|link]]
	- It is an object storage
	- It stores results of calculations / large objects. One process can save results here so another one can read them.
	- Tasks don’t pass big objects via network but by reference to plasma memory.
- Worker processes - [[Ray - Worker processes]]
	- Python worker processes that actually run your task/actor code.
	- They’re started on-demand by the Raylet (not all run all the time).
	- Can be many per node, depending on task concurrency.

**The following processes runs only on the Head node:**
- GCS (Global Control Store) - [[Ray - GCS (Global Control Store)|link]]
	- Cluster metadata, scheduling decisions, resource registry
- Dashboard (optional) - [[Ray - Dashboard|link]]
	- UI for monitoring

For more information about how Raylet and Worker processes are used, refer to the ‘Actors’ and ‘Tasks’ sections in this document.