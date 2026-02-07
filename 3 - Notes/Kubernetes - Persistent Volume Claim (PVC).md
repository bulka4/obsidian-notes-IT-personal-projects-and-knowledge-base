Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
In order to mount a PV (persistent volume) into a pod, we need a PVC (persistent volume claim).

We define it like that:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: managed-csi  # Use Azure disk for data storage
  resources:
    requests:
      storage: 5Gi
```

and mount it:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-using-pvc
spec:
  containers:
  - name: app
    ...
    volumeMounts:
    - name: storage
      mountPath: /data   # Path inside container
  volumes:
  - name: storage
    persistentVolumeClaim:
      claimName: my-pvc
```

In PVC we specify where data will be stored, what kind of storage we want, for example a cloud disk, but we can't choose a specific location where data will be saved. In a PV we can specify where exactly data will be stored.

When we use a PVC to mount at PV to a pod, Kubernetes will automatically choose a proper existing PV or create a new one, if it doesn't exist and dynamic storage provisioning is enabled.