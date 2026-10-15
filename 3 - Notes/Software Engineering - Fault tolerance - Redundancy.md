Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Redundancy means having extra components or resources so that in case of a failure they can start be using instead of failed ones and the system can continue working.

The idea:
> "Do not depend on a single component; have another one that can take over."

For example, we can have a spare server / application replica that can handle workloads in case when one fails.
# Common types
- Component redundancy - Multiple instances of a service
- Data redundancy - Multiple copies of data
- Infrastructure redundancy - Multiple resources:
	- availability zones
	- servers
	- network paths
# How to obtain redundancy
## Replication
Replication ([[Software Engineering - Fault tolerance - Replication|link]]) is one way to create redundancy, for example:
- Create copies of a database
- Run multiple instances of an application
## Backup component (cold standby)
We can have an extra component that is not actively running, for example a server. There is redundancy (a spare server), but no replication happening continuously.
## Redundant network paths
Instead of one network connection, we can have two and if one path fails, the other works.

The network paths are not replicas of each other; they are alternative resources.
