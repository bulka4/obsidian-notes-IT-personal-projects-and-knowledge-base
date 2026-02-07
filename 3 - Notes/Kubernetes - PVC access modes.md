Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
A PVC declares what kind of access a pod needs to a volume. There are 3 modes:
- RWO - ReadWriteOnce
	- Volume can be mounted in read/write mode by only one node at a time (multiple pods on the same node can share that volume)
- ROX / RO - ReadOnlyMany
	- Volume can be mounted in read-only mode into multiple pods (on multiple nodes) at the same time
- RWX - ReadWriteMany
	- Volume can be mounted in a read/write mode into multiple pods (on multiple nodes) simultaneously

Which access mode is supported depends on what storage we use for the PVC (Azure Disk, AWS EBS, GCE PD etc).