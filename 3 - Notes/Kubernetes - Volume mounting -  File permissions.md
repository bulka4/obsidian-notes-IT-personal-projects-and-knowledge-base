Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Propagating file permissions
File permissions which we set up in:
- The data storage used for the volume 
- Any pod having that volume mounted
Are propagated (take effect) to data storage and all the pods.
# Different data storage types
How file permissions behave when using mounting, depends on what data storage (filesystem) we use for the volume. Some of them supports POSIX permissions ([[POSIX-like ACL|link]]), others doesn't.
## Native Linux filesystems
Native Linux filesystem is saved on a disk and permissions to files as well. When we set permissions in that filesystem and mount it into a pod, they are relevant in the pod as well.

We can also modify permissions in a pod and they will become relevant in the mounted filesystem as well.
## SMB-based filesystems
SMB-based filesystems (for example Azure File Share) do not support POSIX permission.
## HostPath
If we use hostPath in the volume (data stored on the filesystem of the localhost), then we can't change file permissions in pods. We need to change them on the localhost and then they will be reflected in pods.
# Setting up permissions for the mounted volume
We can use `securityContext.fsGroup` setting to allow a specific user group to write to all the mounted folders as described here - [[Kubernetes - Security Context|link]].