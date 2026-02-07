Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
## Native Linux filesystems
Native Linux filesystem is saved on a disk and permissions to files as well. When we set permissions in that filesystem and mount it into a pod, they are relevant in the pod as well.

We can also modify permissions in a pod and they will become relevant in the mounted filesystem as well.
## SMB-based filesystems
SMB-based filesystems are for example Azure File Share. They do not support POSIX permission (like native Linux filesystems).