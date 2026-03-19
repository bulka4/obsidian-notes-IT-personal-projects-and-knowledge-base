Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
If we want to run many pods which share the same PV, it is the best practice to schedule all those pods on the same node and use `hostPath` in the PV to save data on the host.

If pods are running on different nodes, they can't reuse the same PV. 

By default no pods can be ran on the control plane (there are taints set), so if we create only one worker, then all the pods will run only on it.

To specify the where on the host PV data will be saved, we need to specify in the `kind-config.yaml`:
```yaml
nodes:
  - role: worker
    # Mount host folders into the node container so it can be mounted into pods
    extraMounts:
      # Airflow DAGs
      - hostPath: "host_path"
        containerPath: container_path  # This path can be used in a PV as a hostPath
```
and in the PV:
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: <name>
  namespace: <namespace>
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  hostPath: 
	  path: container_path
```

Then PV's data will be saved on the host at the `host_path` path.